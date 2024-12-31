---
layout: post
title: "Using the ZooKeeper-Shell to Connect to a ZooKeeper Instance"
author: andre
categories: [ kafka ]
tags: [zookeeper, macOS, kafka]
image: /assets/images/feature-images/feature-image-kafka.jpg
description: This post provides a step-by-step guide to using the ZooKeeper shell for connecting to and interacting with a ZooKeeper instance effectively.
comments: true
---

- Table of Contents
{:toc .large-only}

The ZooKeeper shell serves as an essential tool for seamlessly connecting to and navigating a ZooKeeper instance, 
offering users a comprehensive set of commands to manage and monitor data. This interactive interface simplifies the 
complexities of distributed systems, making it indispensable for those aiming to harness the full potential of 
ZooKeeper's coordination capabilities.

This post provides a step-by-step guide to using the ZooKeeper shell for connecting to and interacting with a ZooKeeper instance effectively.

## What is Zookeeper Shell?
The ZooKeeper shell is an interactive command-line interface that allows users to connect to and interact with a 
ZooKeeper ensemble. It provides a suite of commands to navigate, read, and manipulate the data stored within ZooKeeper's 
hierarchical namespace. 

From listing nodes and retrieving metadata to managing configurations, the ZooKeeper shell offers a direct window into 
the operations and state of the ZooKeeper service. It's an invaluable tool for administrators and developers to monitor, 
debug, and manage the distributed coordination provided by ZooKeeper.

## Explore Zookeeper

### Step 1: Start Zookeeper
Setting up a Kafka environment with a single ZooKeeper node and multiple Kafka brokers offers a rich playground to 
explore the intricacies of ZooKeeper's role in Kafka's distributed architecture. 

Use the following article as guidance on how to configure and setup a Single Zookeeper Node and multi Kafka Broker 
cluster:
* [Setup a Single Zookeeper Node multi Kafka Broker Cluster](/setup-a-single-node-multi-broker-cluster)

```shell
# New Terminal: Start Zookeeper with properties file
$ /usr/local/bin/zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties

# New Terminal: Start Kafka Broker with Server 1 properties file
$ /usr/local/bin/kafka-server-start /usr/local/etc/kafka/server-1.properties

# New Terminal: Start Kafka Broker with Server 2 properties file
$ /usr/local/bin/kafka-server-start /usr/local/etc/kafka/server-2.properties

# New Terminal: Start Kafka Broker with Server 3 properties file
$ /usr/local/bin/kafka-server-start /usr/local/etc/kafka/server-3.properties
```

Once you completed the above article, you should have a single Zookeeper Node and multi Kafka Brokers with a Topic 
called `quote` that will be used in this guide.


### Step 2: Launch ZooKeeper Shell
Launching the `zookeeper-shell` provides a direct interface to interact with your ZooKeeper instance, enabling you to 
manage and inspect znodes, the data nodes that ZooKeeper manages. To initiate the shell, execute the command
`zookeeper-shell {your-zookeeper-server}:{port}`. 

Typically, the default client port for ZooKeeper is `2181`. Once inside the shell, you have a suite of commands at your 
disposal to explore and manipulate the data within ZooKeeper.
```shell
$ zookeeper-shell localhost:2181
```

### Step 3: Basic Commands
ZooKeeper shell commands provide a user-friendly interface to interact with the ZooKeeper ensemble. Through the 
zookeeper-shell, users can perform a variety of tasks directly on the ZooKeeper data store. These commands are 
instrumental for administrators and developers to manage, debug, and monitor the ZooKeeper ensemble, ensuring smooth 
coordination and configuration services in distributed systems.

**Basic Commands**:
- **`ls /`**: Lists the top-level znodes (ZooKeeper nodes).
- **`ls /znode-name`**: Lists the children of the specified znode.
- **`create /new-znode "data"`**: Creates a new znode with the specified data.
- **`get /znode-name`**: Retrieves the data stored in the specified znode.
- **`set /znode-name "new-data"`**: Updates the data of the specified znode.
- **`delete /znode-name`**: Deletes the specified znode.

### Step 4: Explore Zookeeper 


The `ls /` command in the ZooKeeper shell lists the children of the root node in the ZooKeeper hierarchy.
```shell
ls /
[admin, brokers, cluster, config, consumers, controller, controller_epoch, feature, isr_change_notification, latest_producer_id_block, log_dir_event_notification, zookeeper]
```

The `ls /brokers/ids` command in the ZooKeeper shell lists the broker IDs of all active Kafka brokers in the cluster.
```shell
ls /brokers/ids
[1, 2, 3]
```

The `get /brokers/ids/1` command in the ZooKeeper shell retrieves the metadata and configuration details of the Kafka broker with the ID 1.
```shell
get /brokers/ids/1
{"features":{},"listener_security_protocol_map":{"PLAINTEXT":"PLAINTEXT"},"endpoints":["PLAINTEXT://192.168.1.9:9093"],"jmx_port":-1,"port":9093,"host":"192.168.1.9","version":5,"timestamp":"1695021504685"}
```

The `ls /brokers/topics` command in the ZooKeeper shell lists all the topics currently managed by the Kafka brokers in the cluster.
```shell
ls /brokers/topics
[quote]
```

The `get /brokers/topics/{your-topic-name}` command in the ZooKeeper shell retrieves the metadata and configuration details of the specified Kafka topic named {your-topic-name}.
```shell
get /brokers/topics/quote
{"partitions":{"0":[3,2,1]},"topic_id":"SbJQ_jVrRFOYqlkfIgLwNg","adding_replicas":{},"removing_replicas":{},"version":3}
```

For more Zookeeper Shell commands, see the online [Apache Zookeeper CLI Documentation](https://zookeeper.apache.org/doc/r3.6.0/zookeeperCLI.html)

## Summary
The ZooKeeper shell offers a powerful and user-friendly interface to seamlessly connect and interact with a ZooKeeper 
instance. By leveraging its diverse commands, users can efficiently manage, monitor, and debug the data stored within 
the ZooKeeper ensemble.

In essence, mastering the ZooKeeper shell is crucial for anyone working with distributed architectures that rely on 
ZooKeeper.

Happy streaming!

