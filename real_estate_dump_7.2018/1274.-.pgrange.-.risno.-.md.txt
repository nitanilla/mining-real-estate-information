risno
=====

Real-estate search engine. You can try it here : http://risno.org
*risno* stack is based on :

* [elasticsearch][] (v1.5.2)
* [nodejs][] (v0.10.38)

# How to use

Just go to http://risno.org and give it a try.

## Development

A development environment is provided based on [docker](https://www.docker.com). You will first have to [install docker](https://docs.docker.com/installation/).

You will also need GNU Make.

Then clone the git repository. Please prepare your contributions in the develop branch.

    # git clone https://github.com/pgrange/risno.git
    # cd risno
    # git checkout develop

### Start web application

You may want to try the web application with its elasticsearch database using docker and compose.

* Install [compose][] (and [machine][]):

    $ make init

* Launch *risno* and its elasticsearch database:

	$ ./docker-compose up

This command will start an elasticsearch database and the risno web application. Please note that this may take a whiiiiiiile the first time the elasticsearch database container is built since it indexes all french cities and that action takes time.

See docker-compose.yml for details of the containers built and started.

* Open your browser and navigate to `http://localhost:12043` to test the application. Please note that, at this moment, you have no ad indexed so you will not see lot of things.

### Indexing new ads

To index new ads, you may run the *slurp* tool manually. This is not deockerized so it will need some dependencies.

Slurp depends on [nodejs][] at least version 0.12.

To fetch new ads for the supported sites:

    $ cd slurp
    $ make compile
    $ node fetch_sites aquitaine

This will fetch all supported sites for the ads for the french region Aquitaine and index them inside the previously started elasticsearch instance.

Go back to your web browser and see if you can see new ads here `http://localhost:12043/`

### Deployment

You can deploy the whole risno solution with ansible. See ansible sudirectory for details.

## Contributing

See [CONTRIBUTING](CONTRIBUTING.md).


## License

See [LICENSE](LICENSE) for the complete license.


[elasticsearch]: https://www.elastic.co/products/elasticsearch
[nodejs]: https://nodejs.org
[compose]: https://github.com/docker/compose
[machine]: https://github.com/docker/machine
