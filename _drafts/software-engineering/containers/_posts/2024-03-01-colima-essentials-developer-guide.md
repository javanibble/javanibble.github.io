---
layout: post
title: "Colima Essentials Developer Guide"
author: andre
categories: [ software-engineering, containers ]
tags: [colima]
image: /assets/images/feature-images/feature-image-colima.png
description: "Developer Guide for Using the Colima Container Runtime on macOS."
comments: true
---

- Table of Contents
{:toc .large-only}

Dive into the world of Colima with the essentials guide, perfect for getting you started. From easy installation steps to handy command-line tricks, you will learn how to get a local container runtime up and running on your macOS or Linux machine.

Make your development setup smoother and more efficient with Colima!

> UPDATED: Contains updated commands for newer Macs with Apple Silicon.
{:.lead}


## What is Colima?
Colima is a free container runtime available on macOS (and Linux) with minimal setup that can be used to provision 
the Docker container runtime in a Lima VM. Colima has a simple, easy to use command-line interface (CLI) and 
support both Intel and M1 processors.

Other features of Colima includes, support for both `docker` and `containerd` runtimes, port forwarding, volume mounts, 
kubernetes and multiple instances.

Colima can be used as a replacement for Docker Desktop, especially since Docker Desktop is not free under certain 
conditions.

## What is Lima?
Lima is the underlying technology that Colima utilises to achieve its functionality. Lima is an open-source project 
that creates Linux virtual machines (VMs) on macOS, essentially providing a Linux environment on Mac.

Lima launches Linux virtual machines with automatic file sharing, port forwarding and `containerd`. The purpose of 
Lima is to promote `containerd` including `nerdctl` to Mac users.

Lima can also be used for non-container applications. Lima supports both `qemu` and `vz` of running guest machines, 
which can be specified only during instance creation.


## Installing Colima
Colima is available on Homebrew and can be installed on macOS with the following command:

```shell
# Install Colima using Homebrew
$ brew install colima
```

To install Colima making use of MacPorts, Nix, Arch, binaries, or building from the source, following the 
installation guideline on the official [Colima Github](https://github.com/abiosoft/colima/blob/main/docs/INSTALL.md) 
page.

Since Colima can be used as an alternative for Docker Desktop, the following software is required:

```shell
$ brew install docker 
$ brew install docker-compose 
$ brew install docker-credential-helper
$ brew install kubectl
```

## Colima Configuration
### Colima Default Configurations
There are two ways to edit the default configuration, the first is a one-off configuration by starting `colima` with 
the `--edit` flag, and the second is to edit the template for default configurations of new instances.

**One-off Configuration**
```shell
# One-off customisation of the default configuration before startup
$ colima start --edit
```

The config file is located at `$HOME/.colima/default/colima.yaml` and can be configured manually. The configurations 
for other profiles can be found at `$HOME/.colima/<profile-name>/colima.yaml`.

**Template for Default Configuration**
```shell
# Edit the template for default configurations of new instances.
$ colima template
```
The template file is located at `$HOME/.colima/_templates/default.yaml`.

### Configure Docker Login
To ensure `docker login` is properly configured, you need to install `docker-credential-helper`. 
`docker-credential-helper` is a suite of programs to use native stores to keep Docker credentials safe.

You can use the following command to install `docker-credential-helper` on macOS if you have not already done this.

```shell
$ brew install docker-credential-helper
```

After installing `docker-credential-helper` on macOS using Homebrew, the symlink is typically created in Homebrew's 
default binary directory, which is:

```shell
# Newer Macs with Apple Silicon Chips
/opt/homebrew/bin/docker-credential-helper

# Older Macs with Intel Chips
/usr/local/bin/docker-credential-helper
```

To view the symlink and to ensure its configured correct, you can run the following command, and it should show 
something like:

```shell
# Newer Macs with Apple Silicon Chips
$ ls -l /opt/homebrew/bin/docker-credential-osxkeychain

# Older Macs with Intel Chips
$ ls -l /usr/local/bin/docker-credential-osxkeychain
```

The next step is to set the `credstore` property within the `~/.docker/config.json` configuration file to the suffix 
of the program you want to use. For instance, set it to `osxkeychain` if you want to use `docker-credential-osxkeychain`. 
It may be set to something else like desktop.

After you have set the property, the configuration should look as follows:

```json
{
  "credsStore": "osxkeychain"
}
```

### Configure Docker Compose & Volume
To ensure `docker compose` is properly configured, create a `cli-plugin` folder by making use of the following command:

```shell
$ mkdir -p $HOME/.docker/cli-plugins

# Newer Macs with Apple Silicon Chips
ln -sfn /opt/homebrew/opt/docker-compose/bin/docker-compose $HOME/.docker/cli-plugins/docker-compose

# Older Macs with Intel Chips
$ ln -sfn /usr/local/opt/docker-compose/bin/docker-compose $HOME/.docker/cli-plugins/docker-compose
```

### Verify Configuration
To ensure that Colima is successfully installed and configured, the following commands can be used to verify the 
configuration.

Start Colima with the specified container runtime, and run the status command on colima. After Colima was successfully 
started, run the `docker version` command to verify docker is working as the colima runtime.

To ensure the credentials setup is working, run the `docker login` command. The docker-compose version command is 
used to verify Docker Compose is working.

```shell
$ colima start
$ colima status
$ docker version
$ docker login
$ docker-compose version
```


## Colima Examples
### Example: Basic Colima Usage
The basic usage scenario is to start the container runtime via `colima`. If this is the first time you use `colima` a 
new default profile is created with all the default configurations as per the template.

The following properties are the default configurations to be allocated to the virtual machine:

```properties
# Number of CPUs to be allocated to the virtual machine.
cpu: 2
# Size of the disk in GiB to be allocated to the virtual machine.
disk: 60
# Size of the memory in GiB to be allocated to the virtual machine.
memory: 2
# Architecture of the virtual machine (x86_64, aarch64, host).
arch: host
# Container runtime to be used (docker, containerd).
runtime: docker
# Kubernetes configuration for the virtual machine.
kubernetes:
  enabled: false
```

If this is the first time you use docker, you should also log in to the Docker registry. The docker run command can be 
used to run any of the docker containers, in this case its based on the ‘hello-world’ docker image.

Once you are done using docker, you should stop the docker runtime using the `colima stop` command. To ensure all 
instances of colima is stopped, run the `colima list` command.

The following commands is used to perform the basic usage of Colima:

```shell
# Start the default colima instance or create a new default
$ colima start

# List all of the Colima instances
$ colima status

# Log in to a Docker registry.
$ docker login

# Run the docker container called hello-world
$ docker run hello-world
 
# Stop the default colima instance 
$ colima stop

# List all instances of colima 
$ colima list
```

### Example: Manage Colima via Lima CLI
It is possible to manage the colima container runtime within the linux virtual machine via `limactl` in the event that 
the colima tool is not responding.

```shell
# List instances of linux virtual machines.
$ limactl ls

# Stop the Colima linux virtual machine.
$ limactl stop colima

# Delete the Colima linux virtual machine.
$ limactl delete colima

# Display help information about Lima
$ limactl --help
```

## Command Reference
The following commands is based on colima version `0.5.2`. The intent of this section is not to replace the existing 
colima command documentation, but rather serve as a set of commands I regularly use.


**General Information**
- `colima help` - Display help information about the different colima commands.
- `colima completion` - Generate completion script for different shells.
- `colima version` - Print the version of Colima.

**Instance Management**
- `colima start` - Start Colima with the specified container runtime and optional Kubernetes.
- `colima stop` - Stops Colima instance to free up resources. The state of the VM is persisted at stop.
- `colima delete` - Delete and teardown Colima and all settings.
- `colima list` - List all created instances.
- `colima status` - Show the status of Colima.

**Kubernetes Management**
- `colima kubernetes` - Manage Kubernetes cluster.

**SSH and Configuration**
- `colima ssh` - Used to SSH into the VM, or appending additional command runs the command instead.
- `colima ssh-config` - Show configuration of the SSH connection to the VM.
- `colima template` - Edit the template for default configurations of new instances.

**Container Management**
- `colima nerdctl` - Run nerdctl to interact with containerd. (Requires containerd runtime.) 

## Summary
Finally, you have embarked on a detailed exploration of Colima to equip yourself with the knowledge to set up container 
runtimes on macOS efficiently.

This guide is designed to be your companion, helping you unleash the full potential of Colima in your containerisation 
endeavours and overcome any development challenges with greater ease and confidence.