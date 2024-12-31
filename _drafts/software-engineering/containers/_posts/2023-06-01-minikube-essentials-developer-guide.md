---
layout: post
title: "Minikube Essentials Developer Guide"
author: andre
categories: [ software-engineering, containers ]
tags: [minikube]
image: /assets/images/feature-images/feature-image-minikube.jpg
description: "Developer Guide for using Minikube to set up a Kubernetes Cluster on your local machine."
comments: true
---

- Table of Contents
{:toc .large-only}

The Minikube Essentials article provides you with a brief introduction to Minikube. It provides an installation guide 
and command-line commands to set up a local Kubernetes cluster on your local machine (macOS, Linux or Windows).

## What is minikube?
Minikube creates a local Kubernetes cluster on macOS, Linux, and Windows. A production Kubernetes cluster setup consists 
of at least two master nodes and multiple worker nodes on separate virtual or physical machines.

Minikube allows you to run a single-node Kubernetes cluster on your development machine. Both the master and worker 
processes are running on a single node. The docker runtime environment is pre-installed in the node.


## Supported Features
Minikube is a tool that lets you run Kubernetes locally, supporting many core Kubernetes features for development and 
testing. Here’s a list of key Kubernetes features that Minikube supports:

- **Multiple Kubernetes Versions**: Supports switching between different Kubernetes versions.
- **Multi-Node Clusters**: Can simulate a multi-node Kubernetes cluster.
- **Storage Support**: Persistent Volumes (PV), Persistent Volume Claims (PVC), and Dynamic provisioning with local storage
- **Networking**: CoreDNS, LoadBalancer, NodePort services & Ingress support (via addons)
- **Addons**: Dashboard, Ingress (nginx), Metrics-server, Helm, Storage provisioners.
- **Container Network Interface (CNI)**: Supports CNI plugins such as Calico, Flannel, and Cilium.
- **Container Runtime Support**: Docker, containerd, CRI-O
- **Kubernetes API Objects**: Pods, Services, Deployments, StatefulSets, DaemonSets, ConfigMaps and Secrets, HPA
- **Kubernetes API**: Fully supports Kubernetes API access (kubectl, Helm, etc.).
- **Kubernetes RBAC**: Supports Role-Based Access Control (RBAC).

These features make Minikube a highly versatile tool for local Kubernetes development and testing scenarios.

## Installing MiniKube
To install Minikube on macOS with the Homebrew package manager, simply run the following command:

```shell
$ brew install minikube
```

If the which minikube command fails to locate Minikube after installation, you may need to unlink any old Minikube 
versions and link the newly installed binary:

```shell
$ brew unlink minikube
$ brew link minikube
```

For other installation methods and more details, visit the official [Minikube Documentation](https://minikube.sigs.k8s.io/docs/start/).

## Configuration Files
Minikube allows you to deploy custom Kubernetes resources automatically each time Minikube starts by utilising 
deployment files.

The `$MINIKUBE_HOME` environment variable points to the `~/.minikube` folder on MacOS, which holds all minikube 
configuration files and cached artifacts. You can set the `$MINIKUBE_HOME` variable by adding the following to your 
shell configuration (e.g. `.bash_profile` or `.zshrc`):

```shell
export MINIKUBE_HOME=$HOME/.minikube
```

After setting and applying this, all Minikube configuration and cache will be stored in your specified `$MINIKUBE_HOME` 
directory. Here are the key paths for various configuration and deployment files:

- **Deployment Files**: `$MINIKUBE_HOME/addons/deployment.yaml`
- **Explicit Config**: `$MINIKUBE_HOME/config/config.json`
- **Default Config**: `$MINIKUBE_HOME/profiles/minikube/config.json`
- **Applied Config**: `$MINIKUBE_HOME/machines/minikube/config.json`

Configuration files can be mounted from your local machine to the Minikube node by placing them in a specific directory. 
For example, if you place a config file in the path `$MINIKUBE_HOME/files/home/config.yaml` on your local system, 
Minikube will automatically mount this file into the Minikube node at `/home/config.yaml`.

This allows you to provide configuration files directly to your Kubernetes nodes or containers running in Minikube 
without manually copying them into the node. It’s useful for injecting custom configurations into the Minikube 
environment.

## Minikube Examples
### Example: Basic Startup
The Basic Startup example starts the local kubernetes cluster and ensure that minikube is up and running. It also 
ensures that all the pods are running as part of the minikube installation.

The kubernetes dashboard is used to see that all the services are running. Finally, the stop command stops the local 
kubernetes cluster.

```shell
# Starts a local Kubernetes cluster
$ minikube start

# List of each hypervisor instance that's running with hyperkit.
$ ps -ef | grep hyperkit

# List all pods across all namespaces in ps output format.
$ kubectl get pods --all-namespaces

# Access the Kubernetes dashboard running within the minikube cluster
$ minikube dashboard

# Stops the running local Kubernetes cluster
$ minikube stop
```

### Example: Deployment Using NodePort
The Minikube NodePort deployment example starts the local Kubernetes cluster and ensures that Minikube is up and running.

It creates a deployment named `application-nodeport` using the `echoserver` image and exposes it via a NodePort service, 
allowing external access to the application.

The Kubernetes dashboard can be used to monitor the deployment and service, ensuring all components are running as 
expected.

Finally, the service and deployment are deleted, and the stop command halts the local Kubernetes cluster.

```shell
# Starts a local Kubernetes cluster 
$ minikube start

# Create a deployment with the name application-nodeport using the echoserver image.
$ kubectl create deployment application-nodeport --image=k8s.gcr.io/echoserver:1.4 

# List a specific deployment with the name application-nodeport
$ kubectl get deployment application-nodeport

# Show details of application-nodeport deployment 
$ kubectl describe deployment application-nodeport

# Create a service object that exposes the deployment using the service type NodePort
$ kubectl expose deployment application-nodeport --type=NodePort --port=8080

# List a specific service with the name application-nodeport
$ kubectl get service application-nodeport

# Show details of application-nodeport service 
$ kubectl describe service application-nodeport

# Option1: Launch the service and access the application via the default browser. (minikube launches browser)
$ minikube service application-nodeport

# Option 2: Use kubectl to forward the port and access application in browser at http://localhost:7080/
$ kubectl port-forward service/application-nodeport 7080:8080

# Access the Kubernetes dashboard running within the minikube cluster
$ minikube dashboard

# Delete the service called `application-nodeport`
$ kubectl delete service application-nodeport

# Delete the deployment called `application-nodeport`
$ kubectl delete deployment application-nodeport

# Stops the running local Kubernetes cluster
$ minikube stop
```

### Example: Deployment Using LoadBalancer
The Minikube LoadBalancer deployment example starts the local Kubernetes cluster and ensures that Minikube is up and running.

It creates a deployment named `application-loadbalane` using the `echoserver` image and exposes it via a LoadBalancer 
service, allowing external access to the application on port `8080`.

The Kubernetes dashboard can be used to monitor the deployment and service, ensuring all components are running as 
expected.

Finally, the service and deployment are deleted, and the stop command halts the local Kubernetes cluster.

```shell
# Starts a local Kubernetes cluster 
$ minikube start

# Create a deployment with the name application-loadbalance using the echoserver image.
$ kubectl create deployment application-loadbalance --image=k8s.gcr.io/echoserver:1.4 

# List a specific deployment with the name application-loadbalance
$ kubectl get deployment application-loadbalance

# Show details of application-loadbalance deployment 
$ kubectl describe deployment application-loadbalance

# Create a service object that exposes the deployment using the service type LoadBalancer
$ kubectl expose deployment application-loadbalance --type=LoadBalancer --port=8080

# List a specific service with the name application-loadbalance
$ kubectl get service application-loadbalance

# Show details of application-loadbalance service 
$ kubectl describe service application-loadbalance

# Option1: Launch the service and access the application via the default browser. (minikube launches browser)
$ minikube service application-loadbalance

# Option 2: Use kubectl to forward the port and access application in browser at http://localhost:7080/
$ kubectl port-forward service/application-loadbalance 7080:8080

# Access the Kubernetes dashboard running within the minikube cluster
$ minikube dashboard

# Delete the service called `application-loadbalance`
$ kubectl delete service application-loadbalance

# Delete the deployment called `application-loadbalance`
$ kubectl delete deployment application-loadbalance

# Stops the running local Kubernetes cluster
$ minikube stop
```

### Example: Logging & Debugging
This Minikube example demonstrates various commands to start a local Kubernetes cluster with different log verbosity 
levels, retrieve logs for debugging, and use `kubectl` to list and describe pods across namespaces, providing detailed 
insights into cluster operations and potential issues.

```shell
# Starts a local Kubernetes cluster with log level verbosity of 0
$ minikube start --v=0

# Starts a local Kubernetes cluster with log level verbosity of 7 & log to standard error as well as files
$ minikube start --v=7 --alsologtostderr

# Gets the logs of the running instance, used for debugging minikube.
$ minikube logs

# Gets the logs of the running instance, show only log entries which point to known problems
$ minikube logs --problems

# List all pods across all namespaces in ps output format.
$ kubectl get pods --all-namespaces

# Show detailed information about a po with a specific name and namespace.
$ kubectl describe pod <pod name> -n <namespace>
```

### Example: Minikube Addon Management
This Minikube example demonstrates various commands to manage addons within the Minikube cluster, such as enabling and 
disabling features like the Kubernetes dashboard and ingress controller.

It also shows how to check the status of addons, allowing users to easily control and monitor additional cluster functionalities.

```shell
# Lists all available Minikube addons as well as their current statuses
$ minikube addons list

# Enable the dashboard addon for cluster monitoring
$ minikube addons enable dashboard

# Enable the ingress addon for HTTP routing
$ minikube addons enable ingress

# Check the status of the enabled addons
$ minikube addons list

# Disable the dashboard addon when it's no longer needed
$ minikube addons disable dashboard
```

### Example: Minikube Profile Management
This Minikube example demonstrates how to create and manage multiple profiles, enabling users to isolate different 
Kubernetes environments for various use cases, such as development and production.

It includes commands for starting, switching, listing, and deleting profiles, offering flexibility to manage separate 
configurations within the same system.

```shell
# Start a new Minikube profile named "dev"
$ minikube start -p dev

# List all existing Minikube profiles
$ minikube profile list

# Switch to a different Minikube profile
$ minikube start -p prod

# Delete a specific Minikube profile and its associated resources
$ minikube delete -p dev

# Stop a running profile to free up system resources
$ minikube stop -p prod
```

## Command Reference
The Minikube Command Index section provides a list of all available Minikube commands, organized by function for easier
navigation. The set of minikube commands were based minikube version: `v1.34.0`.

**Basic Commands**
* [`minikube start`](https://minikube.sigs.k8s.io/docs/commands/start/) - Initializes and starts a local Kubernetes cluster with options. 
* [`minikube status`](https://minikube.sigs.k8s.io/docs/commands/status/) - Displays the status of the Minikube cluster and its components.
* [`minikube stop`](https://minikube.sigs.k8s.io/docs/commands/stop/) - Stops the running Minikube cluster and frees system resources.
* [`minikube delete`](https://minikube.sigs.k8s.io/docs/commands/delete/) - Deletes the Minikube cluster and removes associated resources.
* [`minikube dashboard`](https://minikube.sigs.k8s.io/docs/commands/dashboard/) - Opens the Kubernetes dashboard in the default web browser. 
* [`minikube pause`](https://minikube.sigs.k8s.io/docs/commands/pause/) - Pauses all running Kubernetes pods in the Minikube cluster.
* [`minikube unpause`](https://minikube.sigs.k8s.io/docs/commands/unpause/) - Unpauses all previously paused Kubernetes pods in the cluster.

**Images Commands**
* [`minikube docker-env`](https://minikube.sigs.k8s.io/docs/commands/docker-env/) - Configures environment to use Minikube's Docker daemon locally.
* [`minikube podman-env`](https://minikube.sigs.k8s.io/docs/commands/podman-env/) - Configures environment to use Minikube's Podman service locally.
* [`minikube cache`](https://minikube.sigs.k8s.io/docs/commands/cache/) - Manages cached images for faster container deployments in Minikube.
* [`minikube image`](https://minikube.sigs.k8s.io/docs/commands/image/) - manages container images within Minikube.

**Configuration and Management Commands**
* [`minikube addons`](https://minikube.sigs.k8s.io/docs/commands/addons/) - Manages Minikube addons for enhanced cluster functionality.
* [`minikube config`](https://minikube.sigs.k8s.io/docs/commands/config/) - Manages Minikube configuration settings and preferences.
* [`minikube profile`](https://minikube.sigs.k8s.io/docs/commands/profile/) - Manages multiple Minikube profiles for different environments.
* [`minikube update-context`](https://minikube.sigs.k8s.io/docs/commands/update-context/) - Updates the Kubernetes context for the current Minikube cluster.

**Networking and Connectivity Commands**
* [`minikube service`](https://minikube.sigs.k8s.io/docs/commands/service/) - Accesses a service in the Minikube cluster via a URL.
* [`minikube tunnel`](https://minikube.sigs.k8s.io/docs/commands/tunnel/) - Creates a network tunnel to expose services in Minikube.

**Advanced Commands**
* [`minikube mount`](https://minikube.sigs.k8s.io/docs/commands/mount/) - Mounts a host directory into the Minikube VM.
* [`minikube ssh`](https://minikube.sigs.k8s.io/docs/commands/ssh/) - Accesses the Minikube VM via SSH for troubleshooting.
* [`minikube kubectl`](https://minikube.sigs.k8s.io/docs/commands/kubectl/) - Invokes kubectl commands using the Minikube context.
* [`minikube node`](https://minikube.sigs.k8s.io/docs/commands/node/) - Manages Minikube cluster nodes and their configurations.

**Troubleshooting Commands**
* [`minikube ssh-key`](https://minikube.sigs.k8s.io/docs/commands/ssh-key/) - Displays the SSH key for accessing the Minikube VM.
* [`minikube ip`](https://minikube.sigs.k8s.io/docs/commands/ip/) - Displays the IP address of the Minikube cluster.
* [`minikube logs`](https://minikube.sigs.k8s.io/docs/commands/logs/) - Retrieves logs from the Minikube cluster for debugging.
* [`minikube update-check`](https://minikube.sigs.k8s.io/docs/commands/update-check/) - Checks for updates available for the Minikube installation.
* [`minikube version`](https://minikube.sigs.k8s.io/docs/commands/version/) - Displays the current Minikube version information.

**Other Commands**
* [`minikube completion`](https://minikube.sigs.k8s.io/docs/commands/completion/) - Generates shell completion scripts for Minikube commands.
* [`minikube help`](https://minikube.sigs.k8s.io/docs/commands/help/) - Displays help information for Minikube commands and usage.
* [`minikube options`](https://minikube.sigs.k8s.io/docs/commands/options/) - Displays global options available for Minikube commands.


## Summary
Finally, you have embarked on a detailed exploration of Minikube to equip yourself with the knowledge to set up a 
Kubernetes Cluster on your local machine.

This guide is designed to be your companion, helping you unleash the full potential of Minikube in your containerisation
endeavours and overcome any development challenges with greater ease and confidence.