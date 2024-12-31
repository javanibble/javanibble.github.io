---
layout: post
title: "The Ultimate Docker Reference"
author: andre
categories: [ Docker ]
tags: [docker, cli]
image: assets/images/feature-images/feature-image-docker.jpg
description: "The Docker CLI Essentials article provides you with a brief introduction to Docker. It provides an installation guide and command-line commands for different scenarios used within the management of docker images and containers."
comments: true
---

- Table of Contents
  {:toc .large-only}

The Docker CLI Essentials article provides you with a brief introduction to Docker. It provides an installation guide and command-line commands for different scenarios used within the management of docker images and containers.

## What is Docker?
> “” ~ [Wikipedia][1]


## Installation
The following links contain guides on how to install docker on your machine:
* [Java Nibble: How to Install Docker on macOS using Homebrew](https://www.javanibble.com/how-to-install-docker-on-macos-using-homebrew/)


## Common Docker Command Scenarios
There are a number of common scenarios where developers make use of docker to perform certain functions. It is through these
common scenarios that we get to appreciate the flexibility and power that docker provides.


---
## Docker Command Reference

### Docker Help Commands
```shell
# Display the help information for the docker command.
$ docker --help

# Display the help information for the docker image command.
$ docker image --help

# Display the help information for the docker image ls command.
$ docker image ls --help
```

---
### Docker Image Commands
The `docker image` command manage Docker Images.

**docker image build**

The `docker image build` command builds an image from a Dockerfile.
```shell
# Build an image from a Dockerfile with a name and optional tag.
$ docker image  build -t {IMAGE_NAME} .
```

**docker image history**
The `docker image history` command shows the history of an image.
```shell
# Show the history of the docker image.
$ docker image history {IMAGE_NAME}

# Show the history of the docker image with Print sizes and dates in human readable format
$ docker image history --human {IMAGE_NAME}
```

**docker image import**


##### docker image inspect
The `docker image inspect` command displays detailed information on one or more images
```shell
# Display information about the {IMAGE_NAME} 
$ docker image inspect {IMAGE_NAME} 
```


##### docker image load

##### docker image ls
The `docker image ls` command list docker images.
```shell

```

##### docker image prune
The `docker image prune` command remove unused images.
```shell
# Remove unused docker images. 
$ docker image prune

# Remove all unused images, not just dangling ones
$ docker image prune --all

# Remove unused docker images, based on the filter criteria: until=<timestamp>
$ docker image prune --filter="until=24h"

# Remove unused docker images, based on the filter criteria: label=<key>=<value>
$ docker image prune --filter="label=deprecated"
$ docker image prune --filter="label=maintainer=john"

# Removed unused docker images, Do not prompt for confirmation
$ docker image prune --force
```

##### docker image pull

##### docker image push

##### docker image rm
The `docker image rm` command remove one or more images. [See Docker Docs](https://docs.docker.com/engine/reference/commandline/image_rm/)
```shell
# Remove a docker image with the name {IMAGE_NAME} 
$ docker image rm {IMAGE_NAME}

# Remove multiple docker images with the name {IMAGE_NAME_1} and {IMAGE_NAME_2} 
$ docker image rm {IMAGE_NAME_1} {IMAGE_NAME_2}

# Force removal a docker image with the name {IMAGE_NAME}
$ docker image rm --force {IMAGE_NAME}

# Remove a docker image with the name {IMAGE_NAME}, but do not delete untagged parents
$ docker image rm --no-prune {IMAGE_NAME}
```

##### docker image save

##### docker image tag

---
### Docker Version Commands
The `docker version` command show the docker version information. [See Docker Docs](https://docs.docker.com/engine/reference/commandline/version/)
```shell
# Print version information and quit
$ docker --version

# Show the Docker version information
$ docker version
```

## Resources
* [Docker CLI Reference](https://docs.docker.com/engine/reference/run/)



