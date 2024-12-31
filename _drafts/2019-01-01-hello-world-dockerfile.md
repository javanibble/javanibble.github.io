---
layout: post
title: "Hello World Dockerfile"
author: andre
categories: [ containers ]
tags: [docker, docker image, docker container, dockerfile]
image: /assets/images/feature-images/feature-image-docker.jpg
description: "The article contains a step-by-step guide on how to create a Hello World Dockerfile example. The Dockerfile is used to create a docker image and a docker container that will be executed and echo the words 'Hello JavaNibble!' as output."
comments: true
---

- Table of Contents 
{:toc .large-only}

The article contains a step-by-step guide on how to create a Hello World Dockerfile example. The Dockerfile is used to create a docker image and a docker container that will be executed and echo the words "Hello JavaNibble!" as output.

## What is a Dockerfile?
> “Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.” ~ [Docker Docs][1]

## Getting Started Guide

### Step 1: Create a Dockerfile
Create a file named `Dockerfile` and add the following docker instructions. `echo` command with parameters `Hello JavaNibble!`.

```dockerfile
FROM busybox
CMD ["echo", "Hello JavaNibble!"]
```

The docker instructions are not case-sensitive, however, convention is for them to be UPPERCASE to distinguish them from
arguments more easily. The `FROM` instruction initializes a new build stage and sets the Base Image for subsequent 
instructions. As such, a valid Dockerfile must start with a `FROM` instruction. There can only be one `CMD` instruction 
in a Dockerfile. The CMD instruction has three forms. The `CMD ["executable","param1","param2"]` form is used for this 
example.


## Compile & Run The Example

### 1. Build the Docker Image
Use the following command to build the Docker Image with a name of `hello-javanibble` and a TAG of `1.0.0` specified by 
the `--tag` option. Also ensure the command is executed in the same directory as the `dockerfile`.

```shell
$ docker image build --tag hello-javanibble:1.0.0 .
```

To ensure the Docker Image was created, list all the docker images by using the following command:
```shell
$ docker image ls
```

### 2. Create a Docker Container
Use the following command to create a docker container with the name `hello-javanibble`.

```shell
$ docker container create --name hello-javanibble hello-javanibble:1.0.0
```

To ensure the Docker Container was created, list all the docker containers (including non-running) by using the 
following command:
```shell
$ docker container ls --all
```

### 3. Start the Docker Container
Use the following command to start the docker container with the name `hello-javanibble`.

```shell
$ docker container start hello-javanibble
```

It is also possible to combine the `docker container create` and `docker container start` command with a single 
`docker container run` command. The `--rm` option will automatically remove the container when it exits.
```shell
$ docker container run --rm hello-javanibble:1.0.0
```

## Example Code
The source code used in this example can be found on [Github][GitHub_Source].

## Finally
Congratulations !!! You have successfully created a Dockerfile based on the Busybox DockerImage that executes the `echo`
command that outputs the strings `Hello JavaNibble!` that are passed to it as arguments. This explains the basic Helloworld
example for Docker using the Dockerfile.

[1]:https://docs.docker.com/engine/reference/builder/
[GitHub_Source]:https://github.com/javanibble/docker-dockerfile-examples/tree/master/hello-world-example