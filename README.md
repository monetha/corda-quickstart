# Corda quickstart

Using this repo you can start Corda locally on your machine using Docker

## Requirements

You need to have the following tools:
- Docker (atleast version 17.09.0 and up) - you can find instructions [here](https://docs.docker.com/install/) on how to install it on your machine.
- docker-compose

## How to start the network

**Please note** that all mentioned commands should be run in the root of this repository.

First run the following commands to initialize node configuration:
```shell
docker build --rm -t corda-tools-boostrapper ./docker/bootstrapper/
docker run -it --rm -v "$PWD/config":/source -w /source corda-tools-boostrapper
```

When the configuration is prepared, you can run the following command to start the Corda network:
```shell
docker-compose up -d
```

To check the port mappings of the nodes, you can use the following command:
```shell
docker-compose ps
```

To remove the network, run the following command:
```shell
docker-compose down
```

## Change node configuration

If you need to change the node configuration, you can do that by editing `*_node.conf` files in `config` directory.
Before doing any changes, run the following command to stop the nodes:
```shell
docker-compose stop
```

After you update the configuration, you should run the `docker run -it --rm -v "$PWD/config":/source -w /source corda-tools-boostrapper` command to modify the node configuration directories.
When the tool is done its work, run the following command to bring the nodes back up:
```shell
docker-compose start
```


## Check if the network is working

In order to verify that the network is up and running, you can connect to Corda SSH service.

First of all, run `docker-compose ps` and get the host mapping of `PartyA` containers port 12222. When you have that value, you can connect to it using a SSH client:
```shell
ssh user1@localhost -p <PartyA SSH port>
Password authentication
Password: 


Welcome to the Corda interactive shell.
Useful commands include 'help' to see what is available, and 'bye' to shut down the node.

Mon Sep 02 00:54:53 GMT 2019>>> run networkMapSnapshot
```
**Please note** you can lookup/change the password in the `Party*_node.conf` file.