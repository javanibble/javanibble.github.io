---
layout: post
title: "Remove Apache Kafka on macOS using Homebrew"
author: andre
categories: [ software-engineering, data-platform ]
tags: [apache-kafka]
image: /assets/images/feature-images/feature-image-kafka.jpg
description: A step-by-step guide on removing Apache Kafka on your local macOS using the Homebrew CLI.
comments: true
---

- Table of Contents
{:toc .large-only}

This guide aims to provide you with a step-by-step process to remove Apache Kafka on macOS using Homebrew.

Apache Kafka is a popular open-source stream-processing software platform developed by the Apache Software Foundation. 

If you’ve installed Kafka and ZooKeeper on your macOS using Homebrew, cleaning up the environment requires a few specific steps. It’s essential to note that the following procedure is tailored for setups where Kafka and ZooKeeper were installed via Homebrew.

## Step 1: Stop Kafka and ZooKeeper Services
Before uninstalling, ensure that both Kafka and ZooKeeper services are stopped.
```shell
$ brew services stop kafka
$ brew services stop zookeeper
```

## Step 2: Uninstall Kafka and ZooKeeper
Use Homebrew to uninstall both Kafka and ZooKeeper.
```shell
$ brew uninstall kafka
$ brew uninstall zookeeper
```

## Step 3: Remove Data and Logs
Kafka and ZooKeeper store logs and data in directories. You might want to remove these to clean up completely.
```shell
$ rm -rf /usr/local/var/lib/kafka-logs
$ rm -rf /usr/local/var/lib/zookeeper
```

## Step 4: Remove Additional Configuration Files
If you've made custom configurations or if there are any residual files, you might want to remove them.
```shell
$ rm -rf /usr/local/etc/kafka
$ rm -rf /usr/local/etc/zookeeper
```

## Step 5: Clean Homebrew Cache
Homebrew caches downloads in a directory. If you want to remove the cached Kafka and ZooKeeper files, you can clean the cache.
```shell
$ brew cleanup kafka
$ brew cleanup zookeeper
```

## Step 6: Check for Residual Processes
Sometimes, even after stopping services, some processes might still be running. Use the `ps` command to check for any 
running Kafka or ZooKeeper processes and terminate them if necessary.
```shell
$ ps aux | grep kafka
$ ps aux | grep zookeeper
```

By following these steps, you should have a clean environment free from Kafka and ZooKeeper installations and 
configurations. If you wish to reinstall later, you can simply use Homebrew to install them again.
* [Install Apache Kafka on macOS using Homebrew](/install-apache-kafka-on-macos-using-homebrew)

## Summary
Removing Kafka on macOS is straightforward using Homebrew. With just a few commands, you can have Kafka and Zookeeper 
completely removed your machine.

