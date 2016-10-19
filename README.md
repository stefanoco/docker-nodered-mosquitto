# Docker composer recipe for Node-RED + Mosquitto + microservices discovery with Consul

Want to play with the latest Node-RED additions in a safe place without
installing and configuring a real host? Docker and composer are the
right tools.

### What's Docker

Docker needs not so many words (or perhaps too many if you never used it).

Docker is a framework for working with containers on a host. It makes it
possible to describe an environment (virtual host), build its image and
bring that image up as a container without ever modifying the configuration
and structure of the hosting machine.

Of course, building and starting many different containers for giving
life to many different services is the main usage for Docker.

Please [see here](https://www.docker.com/)
for more details.

Installing docker-compose is out of the scope of this example, just
as a (possibly very soon broken) reference I'm currently using
this couple of commands to get the latest docker-composer (as root):

```bash
$ curl -L https://github.com/docker/compose/releases/download/1.8.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
$ chmod +x /usr/local/bin/docker-compose
```

### What's docker-compose

docker-compose is a tool you will never stop using after having discovered it.
It's a set of Python based scripts that can easily manage
building / pulling / bringing up and down Docker based services (images
and running containers) based on a very simple and self documenting
```YAML``` configuration file.

Please [see here](https://www.docker.com/products/docker-compose)
for more details.

Installing docker-compose is out of the scope of this example, just
as a (possibly very soon broken) reference I'm currently using
this couple of commands to get the latest docker-composer (as root):

```bash
$ curl -L https://github.com/docker/compose/releases/download/1.8.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
$ chmod +x /usr/local/bin/docker-compose
```

### What's Consul (and Registrator)

Consul with Registrator is among the most complete and simple to be used
services for microservices discovery and health control.

Consul is a server sitting in the same (virtual) network where your
services will come up and down; Registrator is another server speaking
to your Docker daemon and informing Consul about Docker managed services.

Please [see here](http://gliderlabs.com/registrator/latest/user/quickstart/)
for more details.

### What are we doing here

With this example I'm putting this together:

  - Docker containers for a Node-RED and a Mosquitto servers will be
    created and started, with a well described configuration;
  - Docker containers for Consul and Registrator servers will be
    pulled from available images on the Internet and started;
  - Node-RED will be then available at its usual port 1880 of the
    hosting machine (your portable perhaps) for creating your
    next flow, and playing with its features;
  - while playing with Node-RED you will be able to use the local
    MQTT brocker sitting in the same host offered by the related
    Mosquitto container;
  - Consul and Registrator will inform in a handy web page reached
    at the usual port 8500 of the hosting machine about
    Node-RED and Mosquitto services being up and running

### Where to start

You just need to:

  - install Docker and docker-compose
  - clone this repo and log into its folder
  - build and pull the containers: ```docker-compose build && docker-compose pull```
  - start the services: ```docker-compose up -d``` and enjoy using Node-RED
    by browsing at localhost:1880, while logging running services at
    localhost:8500
  - stop the services: ```docker-compose stop```

In order to be able to check messages created while starting the services
please use ```docker-compose up``` instead of ```docker-compose up -d```,
and hit CTRL+C for stopping.

Your Node-RED flow (the ```flows.json``` file) and related settings
will stay saved inside ```nodered/runtime``` for your reference and backup
purposes.

### Scaling

docker-compose has the ability to scale services very easily, with one
single command you can start more instances of the same service (replicating
docker containers). This is still possible in this recipe but some
modifications must be made, notably to the way the containers now
use and save configuration files on mounted folders from the host. Without
doing this you will end up with conflicts between the instances, and
this is (for now) out of the scope of this example.

### More Node-RED libraries

In case you need to install and use available libraries for Node-RED you
just need to modify the Dockerfile contained inside the ```nodered``` folder
and build again the container.

### Credits

  - http://nodered.org/
  - https://github.com/jllopis/docker-mosquitto
  - https://gist.github.com/dceejay/9435867
