Cloudmesh PBS
======================================================================

Cloudmesh PBS provides an easy mechanism to interface with queuing
systems. It integrates nicely with cmd3 and therefore provides a
convenient shell and commandline interface.

The advantage of Cloudmesh PBS is that it can start pbs jobs on remote
machines while using job templates to do so. Jobs submitted with Cloudmesh PBS are
entered in a local database and their status on the remote machines can be
monitored. Thus even if the job disappears from the queuing system either
due to system issues or because they are long finished a record of it is maintained.
In addition to the cmd3 commandshell we provide a simple python API. A REST
interface is being developed.

Project requirements:
----------------------------------------------------------------------

* cmd3
* cloudmesh_base

Github repository
----------------------------------------------------------------------

The source code can be found at:

* https://github.com/cloudmesh/pbs

Installation
----------------------------------------------------------------------

Installation from pypi
^^^^^^^^^^^^^^^^^^^^^^^

(not yet supported)

The easiest way to install Cloudmesh PBS is with pip. We recommend
that you do it in a virtual environment. Once you have created and
activated a virtualenv you can install cloudmesh_pbs with the
following commands::

  pip install cloudmesh_pbs


Development Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^

::


  mkdir github
  cd github
  git clone git@github.com:cloudmesh/base.git
  git clone git@github.com:cloudmesh/cmd3.git
  git clone git@github.com:cloudmesh/pbs.git
  cd base
  git checkout sh
  python setup.py install
  cd ../cmd3
  git checkout sh
  python setup.py install
  cd ../pbs
  python setup.py install

Any change in the program requires a new setup.

Tests::

    python setup.py install; python cloudmesh_job/test_jobdb.py

TODO: other tests to be defined



Usage
----------------------------------------------------------------------

Service Access Specification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When dealing with remote services we often need to customize
interfaces and access. Instead of completely reinventing a
specification file, we are leveraging the ssh config file for
the remote login to the servers. Second we have defined a simple yaml
file that allows us to set up some service specific items. At this time
it supports the specification of jobs submitted through various
supercomputers that are either managed individually through queues,
through groups of queues that are managed for multiple machines in a
single management node.

SSH Config
~~~~~~~~~~~~~~~~~~~~~~~~

We assume that you have set up all machine in ssh config that you like
to access with a simple keyword. For example, if you like to access the
machine cluster.example.com on which you have the username albert then
you have to set up the machine as follows in the ssh config file::

  Host cluster
     Hostname cluster.example.com
     User albert

Naturally you need to place your public key in the authorized_hosts files
on the cluster, you will be able to log into the machine with::

  ssh cluster

To execute command remorely you can specify them in the ssh command.
Here is an example the executes uname -a on the cluster machine::

  ssh cluster uname -a

You should be able to also verify if you can execute the command qstat
with::

  ssh cluster qstat

If this all works you can specify a yaml file for cloudmesh_pbs. We
have included a sample yaml file in the etc directory of the source
code that you can modify accordingly. If we use the example you will
have::

  meta:
    yaml_version: 2.1
    kind: pbs
    cloudmesh:
      pbs:
        cluster:
          manager: cluster
          scripts: ~/qsub/india
          queues:
          - batch
          - long

This file is placed in the directory ~/.cloudmesh

The important part of the file is in the cloudmesh - pbs portion. Here
the name of the machine that we used in .ssh/config is used,
e.g. cluster. The manager allows to specify a manager proxy in case
the machine does not have a dedicated login node from which you can run qstat.
E.g. this is the machine on which the qsub and qstat commands are
executed for this machine. If the management node is different it can
be specified here. The scripts attribute specifies where the pbs
scripts are placed on the remote machine before they are submitted.
To add specific queues you simply can include them as a list in the
queues attribute

.. note:: queue management will be enhanced

API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The API to interface with the queues is straight forward and
documented in more details here::

  TBD

A simple example will show you how to submit a job and check upon its
status. First we define a default host::

    host = "india" 

Next we declare the pbs instance that we use to interact with the
various systems. Upon creation it reads the ssh config file and the
cloudmesh yaml file::

    pbs = PBS(deploy=True)

 Next we find the manager of the host that we use to copy and to
 initiate the pbs commands on::
    
    manager = pbs.manager(host)

let us create on that host the directory ~/scripts/test::
  
    xmkdir(manager, "~/scripts/test")

Now we need to create a pbs job script. For this we use a template that
we have in the etc directory::

    script_template = pbs.read_script("etc/job.pbs")

the template contains the ability to replace the script with some real
commands. Let us use the uname command::
  
    script = """
    uname -a
    """

Also we want to give the job a unique id. For that we maintain in pbs
an internal variable that will be increased every time we submit a
job. We do it here with the incr command::

    pbs.jobid_incr()
    jobname = "job-" + pbs.jobid_get()
    job_script = pbs.create_script(jobname, script, script_template)

Let us now submit the job to the given host::

    r = pbs.qsub(jobname, host, script, template=script_template)

it will return the information of the job. Optionally one can define
an output format (see the API) such as a dict or  a yaml
representation. To optain the PBS variable list as a dict we can use:: 

    d = pbs.variable_list(r)


Status of the job
~~~~~~~~~~~~~~~~~~~~~~~~

The status of a job can be obtained with::

  r = jobstatus(self, host, jobid)

It will not only include the status, but also the environment
variables the job is executed in. 
  

Termination of the Job
~~~~~~~~~~~~~~~~~~~~~~~~~

TBD

Listing of all jobs
~~~~~~~~~~~~~~~~~~~~~~~~~~

TBD

Persistent Database
~~~~~~~~~~~~~~~~~~~~~~~~~~

TBD

Cloudmesh integration
~~~~~~~~~~~~~~~~~~~~~~~~~~

TBD

Swagger
--------------------------

Often we need to document REST APIs that we write so others can look
up their usage. Swagger is a tool that allows us to do that while
augmenting the code with meta data. For Python there are multiple
options to generate REST APIs. One of them is with The
FlaskRestful (https://flask-restful.readthedocs.org/en/0.3.2/).
There is also an extension that allws to integarted swagger into the
tool (https://github.com/rantav/flask-restful-swagger).

To use the tools I recommend to first install the swagger ui on your
local machine. This can be done as follows::

  mkdir -p ~/github
  cd ~/github
  git clone https://github.com/swagger-api/swagger-ui.git
  cd swagger-ui
  open dist/index.html

where opne is the command to open a web browse (on OSX this is open
;-) ) This will open up the swagger user interface in the browser.
Now you can past and copy your api documentation of the code that you
generate.

The cloudmesh_pbs code contains a file called server.py. YOu can start
the server in a second terminal. we assume you have checked out the
codse and configured cmd3 accordingly. We are not describing here hwo
to change the cmd3.yaml file. This can be found elsewhere::

  cd ~/github
  git clone https://github.com/cloudmesh/pbs.git
  cd pbs
  python cloudmesh_pbs/server.py

Now the server is running and we can use the swagger api to look at
it. YOu find the location of the API in the swagger.docs method. There
you find a variable `api_spec_url`. In our case it is
`/pbs/api/spec`. To look at the documentation we just have to prefix
it with our host and port. In our case this is
`http://127.0.0.1:5000`. Hence, you can paste in the
Swagger UI the URL::

  http://127.0.0.1:5000/pbs/api/spec

If everything is done right, you will see the documentation of the
API. Now its just a matter of doing the documentation right. As the
pbs code is under development, this is not yet completed, but it shows
you a simple way on how to get a documentation from a running REST
service via swagger.

Excersises
================

Do not modify server.py, but instead create server-rest.py We want to
maintain server.py as a simple example.

A. complete the pbs implementation with functions that allow to view
   individual jobs and queues by id. Think about routes such as::

     /pbs/job/<host>/<id>
     /pbs/queue/<host>/<id>

   Use for the backend implementation the OpenPBS class

B. Make sure that the right objects are returned in the restful
   implementation. E.g. json objects when asked, ....

C. Identify a mechanism to creat estatic documentation from the
   swagger API in html. This would be useful to be outomatically
   created from a shell script. The output should be written into::

     docs/build/swagger

D. The current implementation does not yet have security. Build upon
   what you learned from A. B. C. To build a secure flask service that
   uses

D. 1. password authentication via https

D. 2. tokenbased authentication

   
Cloudmesh Job
===============

Job management

Job Server
-----------

Start job server::

    cm job server start

Get information::

    cm job server info

Get pid::

    cm job server pid

Terminate the server::

    cm job server stop

Job Script Management
-----------------------

TODO implement

Add Scripts::

    cm job script add FILENAME

Get a Script::

    cm job script get NAME FILENAME

List the Scripts::

    cm job script list

Delete a Script::

    cm job script delete NAMES


Job Management
---------------

Add jobs::

    cm job add ...

Delete job::

    cm job delete ...

List jobs::

    cm job list

List job in json format::

    cm job list --output=json

TODO Update jobs::

    cm job update ID
    cm job update

TODO: Submit a job

    cm job submit job HOST
    cm job submit joblist HOST

Statistics::

    cm job statistics

Exercises:

1. create a number of jobs and submit them to a supercomputer
2. manage the lifecycle of a job


   
   
   





