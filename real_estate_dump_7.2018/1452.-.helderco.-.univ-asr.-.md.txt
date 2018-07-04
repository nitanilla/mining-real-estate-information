# Simulation for a small business network, using Vagrant and Chef

This was made for a class in Network Security and Management. The idea was to configure a small business network according to a set of requirements. These requirements are in `docs/Projecto_Final.pdf` (in portuguese). Our solution is represented in the following diagram.

![Deployment diagram](https://raw.github.com/helderco/univ-asr/master/docs/relatorio/figs/diagrama-deployment.png)

To simulate this network and be able to test the configurations as best we could, we used [Vagrant][] and [Chef][]. In [VirtualBox][], we can simulate the same network using the following setup.

![Vagrant diagram](https://raw.github.com/helderco/univ-asr/master/docs/relatorio/figs/diagrama-virtualbox.png)

## Guide

You need to have [Vagrant][] and [VirtualBox][] installed first.

After that, through the command line, `cd` into the project's folder, and run:

```bash
$ vagrant up
```

This will start to download the base box from the web, start 7 virtual machines, and apply configurations (provision), which includes downloading all necessary packages (e.g. named, http).

You can also up only one machine:

```bash
$ vagrant up dmz
```

Or all client machines using a regular expression:

```bash
$ vagrant up /client*/
```

_Note: The names of these machines are represented in the above diagram._

After doing **up** for the first time, you can skip provisioning to save time:

```bash
$ vagrant up server --no-provision
```

It only makes sense to run **up** when the machine is down. To reboot, use **reload**, or **halt** to shutdown. There's also **suspend** and **resume**. Run `vagrant -h` for available options.

When you're done, you can destroy it all with:

```bash
$ vagrant destroy -f
$ vagrant box remove centos virtualbox
```

The first command removes all virtual machines from disk. The second, removes the base image where the VMs are based off of.

### Using the DNS server externally

During provisioning, the DNS server is automatically updated with the public/external IP attributed to the `dmz`, so that it's possible to access from outside.

There's a script that checks and updates the IP address in the DNS server, in case it has changed. In any case, the current IP address is printed on screen so you can use it to update the list of nameservers in your host machine or any other computer in your LAN that are trying to access the `dmz`.

To find your `dmz` IP:

```bash
$ ./dns.sh
Already up to date for IP 192.168.1.131!
```
If your VM has already been started and that IP changed for some reason (e.g. roaming to another network), you can also restart the interface so that the new IP is updated:

```bash
$ ./dns.sh -r
Determining IP information for eth2... done.
Recovering from backup... done.
Updating files... done.
Stopping named: .[  OK  ]
Starting named: [  OK  ]
Your nameserver is at 192.168.0.105
```

### Accessing through SSH

All the VMs can be accessed through the command `vagrant ssh [vm]`. That access is created automatically by Vagrant through the `eth0` interface, with NAT. This access makes it easier o manage each individual VM, but, to simulate what would happen in production, we should access the DMZ and through it, the rest of the network. Since Vagrant also creates the user `vagrant` with administration privileges, all the VMs make use of this by being the only user that is allowed to ssh to.

To gain root access to the internal server:

```bash
$ ssh vagrant@imbcc.pt
vagrant@imbcc.pt’s password:
[vagrant@dmz ~]$ ssh vagrant@server
vagrant@server’s password:
[vagrant@server ~]# su -
Password:
[root@server ~]#
```

The password for the users `vagrant` and `root` is `vagrant`.

### Shared folder

Vagrant sets up automatically a shared folder at `/vagrant` which points to the current folder in the host machine, where `Vagrantfile` is located. This can be useful to transfer files from the VM to the host machine and vice versa.

### Bootup order

The order in which the VMs are booted up matters, since there's dependencies between them. The VM `dmz` has it's own connection to the Internet e so it can be used independently, except for [ownCloud][] which needs LDAP from `server`.

All other VMs need the `router` to be able to access the Internet and the `dmz` for the DNS, including `router` itself.

This only matters if using `vagrant up [vm]` though. `vagrant up` by itself will boot all VMs in the right order.

### Problems

If a VM doesn't respond when it's being shutdown or booted up, the following error may appear:

    stderr: VBoxManage: error: The object is not ready

If that happens, just keep insisting.

For errors during the _provision_ phase, just keep repeating the provisioning as many times as you want:

```bash
$ vagrant provision server
```

It's built in a way that it tries to make sure the VM is in the intended state.

If a VM can't connect to the Internet it will fail during the _provision_ phase. If the VM has already gone through a completely successful `vagrant up`, then you can skip this phase with the option `--no-provision` as seen at the beginning of this guide.

## Todo

- Make a secure connection with TLS between ownCloud and the LDAP server;
- Use LDAP with FTPS to authenticate:
    - the real estate group (_imobiliária_) into their _userdirs_;
    - the web designers to the `/var/www` dir.

## More information (in portuguese)

O enunciado e relatório está em `docs`.

[Vagrant]: http://www.vagrantup.com
[VirtualBox]: https://www.virtualbox.org
[Chef]: http://www.opscode.com/chef/
[ownCloud]: http://owncloud.org
