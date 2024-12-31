---
layout: post
title: "Docker Image & Repository Essentials"
author: andre
categories: [ containers ]
tags: [docker]
image: /assets/images/feature-images/feature-image-docker.jpg
description: ""
comments: true
---

- Table of Contents
{:toc .large-only}

The Docker Essentials article provides you with

## Docker Architecture
Docker uses a client-server architecture since the docker client and docker daemon is separate binaries. The Docker 
deamon is responsible for buillding, running and distributing the docker containers. The client communicates with the 
daemon via a REST API (Network Interface, Unix Sockets). The docker client can connect to several docker daemons.

* The docker client (`docker`) is used by the user to interact with docker and sends the commands to the docker daemon.
* The docker daemon (`dockerd`) is the persistent process that listens for API requests and manages docker objects like containers, images, volumes, networks, etc... 
* The docker registry stores docker images. DockerHub is a public registry and is used by docker by default to look for images.

![Docker Architecture](/assets/images/posts/docker/docker-overview.png){:.lead width="800" height="100" loading="lazy"}
Docker Overview
{:.figcaption}

**Docker Objects**
* A *docker image* is a template that contains read-only instructions for building a docker container. A Docker image can be composed of other docker images. A Dockerfile consist of a set of instructions that are executed in order to create layers within the image. This allows you to build your own image using a Dockerfile.
* A *docker container* is a runnable instance of a docker image. Docker containers has a well-defined lifecycle, allowing you to create, start, stop, move, or delete a container via the docker client (cli) or docker API. Other features of containers are the ability to attach a container to networks and a persistent storage.
* A *docker service* is a deployment unit describing the desired state of containers in a docker swarm. The service specifies the number of replicas, configuration options, and the network to which containers are attached.

## Docker Objects
One can compare containers and images to Object Oriented programming in that a Docker Image is a class, and the Docker 
Container is the instance of the class.

## Docker Image
A docker image is a template for your containers. A docker image consist of multiple layers stacked on top of each other 
and is seen as design-time constructs. Each layer of a docker image represents an instruction in the Dockerfile. Each 
layer of the docker image is read-only except for the last one. The Docker Image is a combination of all the layers.

## Docker Container
Docker Containers on the other hand are runtime constructs. Docker files are used to built a Docker Image and consist of 
a set of instructions. Containers are meant to be lightweight and hence the Docker Images are supposed to be as small as 
possible. Containers add a new writable (read/write) layer on top of the underlying layers and is referred to as the 
Container Layer. Changes within the running container are made to the Container Layer. The Container Layer 
(writable layer) is deleted when the Docker Container is deleted and the Docker Image and all the layers within the 
image remains unchanged.


## Docker Hub Basics

**What is a Docker Registry?**
A Docker Registry is a storage and content delivery system, holding named Docker images, available in different tagged 
versions. The Docker Registry allows you to control where your Docker Images are stored. Docker Hub is a public Docker 
registry that can be found at [https://hub.docker.com/](https://hub.docker.com/) provided by Docker. Docker Hub is 
similar to GitHub since it enables the public and private hosting of Docker Images.

**What is a Docker Repository?**
A Docker Repository is a collection of different images with the same name within a Docker Registry. The different 
versions of the same docker image is differentiated by tags. The Tag  is an alphanumeric identifier of the image within 
a repository.

**Official Images**
The Docker Official Images are a curated set of Docker repositories hosted on Docker Hub. They provide essential base 
OS repositories (ubuntu, centos) that can be used as base images for your Docker Images. Docker Official Images also 
provide solutions for programming language runtimes, data stores and other services. The Docker Official Images can also 
serve as an example for `Dockerfile` best practices and provide clear documentation to serve as a reference.

**Docker Verified Publisher**
The Docker Verified and Publisher Program enables Independent Software Vendors (ISVs), development tools vendors, and 
platform providers to distribute Dockerized content through Docker Hub.


## Docker Commands
The following commands is based on docker version `20.10.23`. The intent of this section is not to replace the existing
docker command documentation, but rather serve as a set of commands I regularly use.

### Docker Image
The `docker image` command is a management command that is used to manage docker images.

**Help**
* [`docker image --help`](#) list all the docker image commands. [Reference](https://docs.docker.com/engine/reference/commandline/image/)
* [`docker image COMMAND --help`](#) list the explanation, usage, aliases and options for a docker image command.

**Lifecycle**
* [`docker image build`](#docker-image-build) build an image from a Dockerfile. [Reference](https://docs.docker.com/engine/reference/commandline/image_build/)
* [`docker image import`](#) import the contents from a tarball to create a filesystem image. [Reference](https://docs.docker.com/engine/reference/commandline/image_import/)
* [`docker image load`](#) load an image from a tar archive or STDIN. [Reference](https://docs.docker.com/engine/reference/commandline/image_load/)
* [`docker image pull`](#) pull an image or a repository from a registry. [Reference](https://docs.docker.com/engine/reference/commandline/image_pull/)
* [`docker image push`](#) push an image or a repository to a registry. [Reference](https://docs.docker.com/engine/reference/commandline/image_push/)
* [`docker image save`](#) Save one or more images to a tar archive (streamed to STDOUT by default). [Reference](https://docs.docker.com/engine/reference/commandline/image_save/)
* [`docker image tag`](#) Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE. [Reference](https://docs.docker.com/engine/reference/commandline/image_tag/)

**Info**
* [`docker image history`](#) show the history of an image. [Reference](https://docs.docker.com/engine/reference/commandline/image_history/)
* [`docker image inspect`](#) display detailed information on one or more images. [Reference](https://docs.docker.com/engine/reference/commandline/image_inspect/)
* [`docker image ls`](#) list images. [Reference](https://docs.docker.com/engine/reference/commandline/image_ls/)

**Cleaning up**
* [`docker image prune`](#) remove unused images. [Reference](https://docs.docker.com/engine/reference/commandline/image_prune/)
* [`docker image rm`](#) remove one or more images. [Reference](https://docs.docker.com/engine/reference/commandline/image_rm/)


