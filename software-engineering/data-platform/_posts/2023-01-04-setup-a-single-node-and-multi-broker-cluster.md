---
layout: post
title: "Setup a Single Zookeeper Node and a Multi Broker Cluster"
author: andre
categories: [ software-engineering, data-platform ]
tags: [apache-kafka]
image: /assets/images/feature-images/feature-image-kafka.jpg
description: A step-by-step guide on how to setup a single Zookeeper Node and a multi Kafka Broker Cluster.
comments: true
---

- Table of Contents
{:toc .large-only}

This guide aims to provide you with a step-by-step process to setup a single Zookeeper Node and a multi Kafka broker cluster.

In today’s data-driven world, real-time data processing is more crucial than ever. Apache Kafka, a distributed streaming platform, has emerged as a frontrunner in this domain, enabling countless businesses to handle real-time data feeds efficiently.

Setting up Kafka and ZooKeeper on a local machine is an excellent starting point for beginners and developers looking to experiment. This blog explains setting up a single-node ZooKeeper and a multi-broker Kafka cluster on your macOS machine.

So, let’s embark on this journey and transform your local macOS machine into a mini data streaming powerhouse!

## Introduction
In Kafka, a single node multi-broker solution means multiple Kafka brokers are running on a single machine or node, alongside a ZooKeeper instance.

This setup allows for experimentation with broker distribution and topic replication on a single machine, but it doesn’t offer the fault tolerance benefits of a distributed multi-node environment.

<br>
<div style=" vertical-align:middle; text-align:center">
<img width="80%" src="/assets/images/posts/apache-kafka-essentials/single-node-multi-broker-kafka.jpg">
</div>
<br>

In the context of ZooKeeper and Kafka:

- **Single Node (ZooKeeper)**: Refers to running a single instance of ZooKeeper. In a production environment, ZooKeeper typically runs in a replicated mode across multiple nodes for fault tolerance.

- **Multi Broker (Kafka)**: Refers to running multiple instances of Kafka brokers. This setup ensures data redundancy, high availability, and better load distribution across the cluster.

## Installation
There are a number of ways that you can install the Kafka and Zookeeper on your local machine. Use the following link 
to use Homebrew.
* [Install Apache Kafka on macOS using Homebrew](/install-apache-kafka-on-macos-using-homebrew)

## Configuration
The `/usr/local/etc/kafka` directory typically contains the configuration files for Kafka when it's installed on macOS,
especially if you've used a package manager like Homebrew. Within this directory, you'll find various properties files
that dictate how Kafka behaves.

The following command can be used to list all the Kafka properties files.
```shell
$ ls /usr/local/etc/kafka
connect-console-sink.properties   connect-log4j.properties          log4j.properties                  trogdor.conf
connect-console-source.properties connect-mirror-maker.properties   playground.config                 zookeeper.properties
connect-distributed.properties    connect-standalone.properties     producer.properties
connect-file-sink.properties      consumer.properties               server.properties
connect-file-source.properties    kraft                             tools-log4j.properties
```

### Zookeeper Properties
To start a local instance (single node) of ZooKeeper, we'll utilize the configuration file that comes bundled with Kafka, 
located at `/usr/local/etc/kafka/zookeeper.properties`. 

Kafka provides the required property files which defining minimal properties required for a single broker-single node cluster. 

The `/usr/local/etc/kafka/zookeeper.properties` file is used for this purpose. 

No changes to the properties file is required.

### Kafka Properties
To start a local instance (single Broker Cluster) of Kafka, we'll utilize the configuration file that comes bundled with Kafka,
located at `/usr/local/etc/kafka/server.properties`. 

Copy the default server properties to create configurations for each broker:
```shell
$ cp /usr/local/etc/kafka/server.properties /usr/local/etc/kafka/server-1.properties
$ cp /usr/local/etc/kafka/server.properties /usr/local/etc/kafka/server-2.properties
$ cp /usr/local/etc/kafka/server.properties /usr/local/etc/kafka/server-3.properties
```

Modify each of the properties files as follows:
**File: server-1.properties**
```properties
broker.id=1
listeners=PLAINTEXT://:9093
log.dirs=/tmp/kafka-logs-1
```

**File: server-2.properties**
```properties
broker.id=2
listeners=PLAINTEXT://:9094
log.dirs=/tmp/kafka-logs-2
```

**File: server-3.properties**
```properties
broker.id=3
listeners=PLAINTEXT://:9095
log.dirs=/tmp/kafka-logs-3
```

## Testing the Setup
To test the setup of a single-node and single-broker cluster, we first initiate ZooKeeper and Kafka. Once they're 
running, we create a topic within Kafka. After establishing the topic, we set up a publisher to write a message to this 
topic. Concurrently, we introduce a consumer designed to read and display the message. This end-to-end process ensures 
that both ZooKeeper and Kafka are functioning seamlessly together.

### Step 1: Start Zookeeper
Open a new terminal and run the following command:
```shell
# Start Zookeeper with properties file
$ /usr/local/bin/zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```

### Step 2: Start Kafka Brokers
Open a new terminal and run the following command to start Broker 1:
```shell
# Start Kafka with properties file
$ /usr/local/bin/kafka-server-start /usr/local/etc/kafka/server-1.properties
```

Open a new terminal and run the following command to start Broker 2:
```shell
# Start Kafka with properties file
$ /usr/local/bin/kafka-server-start /usr/local/etc/kafka/server-2.properties
```

Open a new terminal and run the following command to start Broker 3:
```shell
# Start Kafka with properties file
$ /usr/local/bin/kafka-server-start /usr/local/etc/kafka/server-3.properties
```


### Step 3: Create a Topic
Create a Kafka Topic called `quote` with 1 partition and a replication factor of 3 since there is three brokers. To do 
this, open a new terminal and run the following command:
```shell
$ kafka-topics --create --topic quote --bootstrap-server localhost:9093 --partitions 1 --replication-factor 3
```

To ensure the topic was created successful, use the following command to describe the Kafka topic called `quote`.
```shell
$ kafka-topics --describe --topic quote --bootstrap-server localhost:9093
```

### Step 4: Produce a Message
Create a console-based Kafka producer to send messages to the `quote` Kafka topic running at `localhost:9093`. To do 
this, open a new terminal and run the following command:
```shell
$ kafka-console-producer --topic quote --bootstrap-server localhost:9093
> To stream, or not to stream: that is a Kafka question ... ~ William Kafka 
```

### Step 5: Consume a Message
Create a console-based Kafka consumer to retrieve messages from the `quote` Kafka topic running at `localhost:9093`. To do
this, open a new terminal and run the following command:
```shell
$ kafka-console-consumer --topic quote --bootstrap-server localhost:9093 --from-beginning
To stream, or not to stream: that is a Kafka question ... ~ William Kafka
```

## Cleanup Kafka Data
Kafka and ZooKeeper store logs and data in directories. You might want to remove these to clean up completely.

Ensure that all the Kafka Brokers and Zookeeper servers are stopped. Then delete the logs and data using the following
commands:
```bash
$ rm -rf /usr/local/var/lib/kafka-logs-1
$ rm -rf /usr/local/var/lib/kafka-logs-2
$ rm -rf /usr/local/var/lib/kafka-logs-3
$ rm -rf /usr/local/var/lib/zookeeper
```

## Summary
In conclusion, understanding and setting up distributed systems like Kafka and ZooKeeper can seem daunting, but it 
becomes a straightforward task with the proper guidance. You've taken a significant step into real-time data processing 
by establishing a single-node ZooKeeper and multi-broker Kafka cluster on your macOS. 

This foundational knowledge will be a springboard for more complex deployments and applications. As you continue 
exploring, remember that the world of distributed systems is vast, and this is just the beginning of an exciting journey. 

Happy streaming!

[Install_Camunda_Modeler]:/how-to-install-camunda-modeler-on-macos-using-homebrew
[1]:https://kafka.apache.org/
