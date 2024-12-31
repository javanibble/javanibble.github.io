---
layout: post
title: "Docker Commands: MySQL"
author: andre
categories: [ containers ]
tags: [docker, cheat sheet, mysql]
image: /assets/images/feature-images/feature-image-docker.jpg
description: "The Docker commands for MySQL contains a list of the docker commands that are frequently used to download, stop and start the docker container containing the MySQL database."
comments: true
---

- Table of Contents
{:toc .large-only}

The Docker commands for MySQL contains a list of the frequently used docker commands. This list includes commands to run, stop and start the docker container containing the MySQL database. The cheatsheet does not provide an exhaustive list of all docker commands, for which you should refer to the official docker documentation page.

## Docker Hub & MySQL Images
Docker Hub is the default registry where Docker looks for images. There are two main MySQL images on Docker Hub, and both include the MySQL community edition. 
* **Official**: The official image, called `mysql`, is built and maintained by the Docker community with the help of the MySQL team. See the [Dockerfile][3] file for details.
* **Oracle**: The image from Oracle, called `mysql-server` is forked from mysql by the Docker team. The image is created, maintained and supported by the MySQL team at Oracle. See the [Dockerfile][4] file for details.

**Note:** The official image will be used for all the docker commands as part of this cheat sheet.

## Quick Commands
The following commands are all you need to get a docker container with MySQL running. This examples also defines the container name, the root password and the port to expose on the host.

```shell
# Creates a container layer over the mysql image and then starts it.
$ docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 -d mysql:latest

# Fetches the logs of the container.
$ docker logs mysql-container

# Executes the mysql command to log into the database
$ docker exec -it mysql-container mysql -uroot -p
```
**Note**: The password is 'password' as set by the first command.

## Docker Commands
The following sections contain a list of the most used docker commands with a MySQL image and container. 

#### Container Lifecycle Commands
The `docker run` command runs a container named `some-mysql` using the `mysql:latest` image. Here is a description of the options:
* The `--detach, -d` option runs the container in background and print container ID.
* The `--env, -e` option sets environment variables. 
* The `--name` option assigns a name to the container.
* The `--publish, -p` option publishes a container’s port(s) to the host.

```shell
# Creates a container layer over the image and then starts it.
# docker run --name <container_name> --env MYSQL_ROOT_PASSWORD=<password> --publish <host_port>:<container_port> --detach <image>
$ docker run --name mysql-container --env MYSQL_ROOT_PASSWORD=password --publish 3306:3306 --detach mysql --performance_schema=ON

# Removes one or more containers.
# docker rm <container>
$ docker rm mysql-container
```

#### Container Start & Stop Commands
The following commands are used to stop, start, restart and kill the docker container. The `<container>` operator identifies the container in three ways, UUID long identifier, UUID short identifier or name.

```shell
# Stops one or more containers.
$ docker stop <container>

# Starts one or more containers.
$ docker start <container>

# Restarts one or more containers.
$ docker restart <container>

# Kills one or more running containers.
$ docker kill <container>
```

#### Container Info Commands
The following commands are used to obtain information about the docker container. The `<container>` operator identifies the container in three ways, UUID long identifier, UUID short identifier or name.

```shell
# Lists all the running containers. (Running Containers)
$ docker ps

# Lists all the running containers. (All Containers)
$ docker ps --all

# Fetches the logs of the container.
$ docker logs <container>

# Lists the port mappings for the container.
$ docker port <container>

# Displays a live stream of the container resource usage statistics.
$ docker stats <container>
```

#### Container Executing Commands
The following commands are used to run commands within the docker container. The `<container>` operator identifies the container in three ways, UUID long identifier, UUID short identifier or name.

```shell
# Runs a bash session inside the running container.
$ docker exec -it <container> bash

# Runs the command to import data from your host machine while keeping STDIN open.
$ docker exec -i <container> sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < /some/path/on/your/host/all-databases.sql
```

#### Images Lifecycle Commands
The following commands are used to manage the lifecycle of a docker image. 

```shell
# Shows all top level images, their repository and tags, and their size.
$ docker images

# Removes one or more images and can be used to remove the MySQL images with specific tags.
$ docker image rm <image>:<tag>
$ docker image rm mysql:latest

# Removes one or more images and can be used to remove the MySQL images with specific tags.
$ docker rmi <image>
$ docker rmi mysql:latest
```

#### Images Info Commands
The following commands are used to provide information of a docker image. 

```shell
# Shows the history of an image.
$ docker history <image>
$ docker history mysql:latest
```

#### Registry & Repository Commands
The following commands are used to navigate, search and retrieve images from the Docker Repository. 
```shell
# Search the Docker Hub for images.
$ docker search <term>
$ docker search mysql

# Pulls the MySQL Community Edition image.
$ docker pull mysql:<tag>
$ docker pull mysql:latest
```

#### Docker Help
The following commands are used to get help via the command line. 
```shell
# Information on the docker command itself.
$ docker --help

# Information on a specific docker command.
$ docker <COMMAND> --help
```

## Docker: MySQL Environment Variables
When you start the mysql image, you can adjust the configuration of the MySQL instance by passing one or more environment variables on the `docker run`  command line.

* `MYSQL_ROOT_PASSWORD`: This variable is mandatory and specifies the password that will be set for the MySQL root superuser account.
* `MYSQL_DATABASE`: This variable is optional and allows you to specify the name of a database to be created on image startup.
* `MYSQL_USER`: This variable is optional, used to create a new user. (Used In Conjunction)
* `MYSQL_PASSWORD`: This variable is optional, used to set the user's password. (Used In Conjunction)
* `MYSQL_ALLOW_EMPTY_PASSWORD`: This is an optional variable. Set to a non-empty value, like yes, to allow the container to be started with a blank password for the root user.
* `MYSQL_RANDOM_ROOT_PASSWORD`: This is an optional variable. Set to a non-empty value, like yes, to generate a random initial password for the root user (using pwgen). The generated root password will be printed to stdout
* `MYSQL_ONETIME_PASSWORD`: Sets root (not the user-specified in MYSQL_USER!) user as expired once init is complete, forcing a password change on the first login.


## Summary
Please feel free to share the Docker cheat sheet for MySQL commands with friends and colleagues. Follow me on any of the different social media platforms and feel free to leave comments.

[3]:https://github.com/docker-library/mysql/blob/bc6e37a2bed792b1c4fc6ab1ec3ce316e6a5f061/8.0/Dockerfile
[4]:https://github.com/mysql/mysql-docker/blob/mysql-server/8.0/Dockerfile