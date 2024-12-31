---
layout: post
title: "Manage Kafka Topics Using Command Line Interface (CLI)"
author: andre
categories: [ kafka ]
tags: [macOS, kafka]
image: /assets/images/feature-images/feature-image-kafka.jpg
description: This guide describes how to manage Kafka topics using the CLI, ensuring you harness the full potential of your Kafka setup.
comments: true
---

- Table of Contents
{:toc .large-only}

Kafka, a distributed streaming platform, plays a pivotal role in handling real-time data streams. Central to Kafka's 
design are "topics" where messages are stored and categorized. While there are various tools and interfaces to manage 
these topics, the Command Line Interface (CLI) stands out as a powerful, direct, and often preferred method. 

This guide describes how to manage Kafka topics using the CLI, ensuring you harness the full potential of your Kafka setup.

## What is Kafka Topics?
In Kafka, messages are organized into categories known as topics, ensuring durable storage. Each topic is further 
divided into multiple partitions. Unlike traditional databases, you can't query messages within a topic. Instead, 
producers write messages to topics while consumers read from them. 

Notably, even after consumption, messages remain intact within a topic, allowing repeated reads, which is a departure 
from conventional messaging systems. Kafka topics are versatile, supporting multiple producers and subscribers; a single 
topic can have numerous producers writing to it and several consumers subscribing to its messages. 

The retention period of a message within a topic is determined by its configuration. Topics, identifiable by their 
unique names, can accommodate messages in various formats, be it JSON, Avro, text, or binary. In Kafka's terminology, 
a sequence of messages is termed a "data stream." Regardless of the number of partitions, a data stream represents a 
single topic of data in Kafka.

## Manage Kafka Topics

### Step 1: Start Kafka Cluster
Setting up a Kafka environment with a single ZooKeeper node and multiple Kafka brokers offers a rich playground to 
explore the intricacies of ZooKeeper's role in Kafka's distributed architecture. 

**Prerequisite**:
* [Setup a Single Zookeeper Node multi Kafka Broker Cluster](/setup-a-single-node-multi-broker-cluster)

**Start Kafka Cluster**

Use the following commands to start the Zookeeper instance and three Kafka Brokers:
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


### Step 2: Basic Commands
The Kafka Topics command-line interface (CLI) is an essential tool for managing and interacting with topics within a 
Kafka cluster. Bundled with Kafka's binary distribution, this CLI provides a suite of commands that allow users to 
create, delete, describe, and alter topics. By using the `kafka-topics` command, users can specify various 
configurations such as the number of partitions, replication factor, and other topic-specific settings. 

**Basic Commands**:
- **`kafka-topics --help`**: Print usage information about the different options.
- **`kafka-topics --bootstrap-server`**: Required: The Kafka server and port to connect to.
- **`kafka-topics --list`**: List all available topics.
- **`kafka-topics --topic <String: topic>`**: The topic to create, alter, describe or delete.
- **`kafka-topics --create`**: Create a new Topic
- **`kafka-topics --delete`**: Delete a Topic
- **`kafka-topics --describe`**: List details for the given topics.
- **`kafka-topics --partitions`**: The number of partitions for the topic being created or altered. If not supplied for create, defaults to the cluster default.
- **`kafka-topics --replication-factor`**: The replication factor for each partition in the topic being created. If not supplied, defaults to the cluster default.

**Remember**:

Take note of the following before executing the commands below:
- **Default Port Number**: The default port number for a single Kafka Broker is `9092`. As part of the multi-broker cluster, these are now `9093`, `9094` and  `9095`.
- **Default Partition Count**: The default number of partitions for a topic, if not specified during topic creation, is 1. This means that, by default, a topic will have a single partition.
- **Default Replication Factor**: The default replication factor, if not specified during topic creation, is 1. This implies that, by default, there's only one copy (or replica) of the data for a topic.


### Step 3: Create Topic
In this step we will create a topic called `Topic_A` within a Kafka Cluster consisting of three Brokers. The partition 
count and replication factor will not be set, and hence the default values will be used. The Kafka cluster decides on 
which Broker the topic will be created and which brokers will have replicas of the topic.   

**Diagram: Kafka Cluster**

The Kafka Cluster with three Brokers and `Topic_A` with a partition count of 1 and a replication factor of 1.

![Kafka Topic - Partitions 2 - Replication 1](/assets/images/posts/manage-kafka-topics/topic_a.jpg)

**Commands:**
```shell
# Create a new topic called Topic_A 
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_A --create

# Describe the topic called Topic_A
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_A --describe
Topic: Topic_A	TopicId: ZwKEWOb8RKqVoLaNMFL7mA	PartitionCount: 1	ReplicationFactor: 1	Configs: 
	Topic: Topic_A	Partition: 0	Leader: 1	Replicas: 1	Isr: 1
```

The output of the command illustrates the `PartitionCount: 1` and `ReplicationFactor: 1`. It also indicates for each
partition of the topic, the Broker ID(s) of the Leader, Replicas and In-Sync Replicas (ISR).

### Step 4: Create Topic with Partitions
In this step we will create a topic called `Topic_B` within a Kafka Cluster consisting of three Brokers. The replication 
factor will not be set, and hence the default value will be used. The partition count is set to `2`. The Kafka cluster 
decides on which Broker the topic will be created and which brokers will have replicas of the topic.

**Diagram: Kafka Cluster**

The Kafka Cluster with three Brokers and `Topic_B` with a partition count of 2 and a replication factor of 1.

![Kafka Topic - Partitions 2 - Replication 1](/assets/images/posts/manage-kafka-topics/topic_b.jpg)

**Commands:**
```shell
# Create a new topic called Topic_B with 2 partitions
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_B --create --partitions 2

# Describe the topic called Topic_B
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_B --describe
Topic: Topic_B	TopicId: jrflStf7RQWJBSSHtv7F9A	PartitionCount: 2	ReplicationFactor: 1	Configs: 
	Topic: Topic_B	Partition: 0	Leader: 1	Replicas: 1	Isr: 1
	Topic: Topic_B	Partition: 1	Leader: 2	Replicas: 2	Isr: 2
```

The output of the command illustrates the `PartitionCount: 2` and `ReplicationFactor: 1`. It also indicates for each
partition of the topic, the Broker ID(s) of the Leader, Replicas and In-Sync Replicas (ISR).

### Step 6: Create Topic with Replication
In this step we will create a topic called `Topic_C` within a Kafka Cluster consisting of three Brokers. The partition 
count is set to `2`. The replication factor is set to `3`. The Kafka cluster decides on which Broker the topic will be 
created and which brokers will have replicas of the topic.

**Diagram: Kafka Cluster**

The Kafka Cluster with three Brokers and `Topic_C` with a partition count of 2 and a replication factor of 3.

![Kafka Topic - Partitions 2 - Replication 3](/assets/images/posts/manage-kafka-topics/topic_c.jpg)

**Commands:**
```shell
# Create a new topic called Topic_C with 2 partitions and a replication factor of 3
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_C --create --partitions 2 --replication-factor 3

# Describe the topic called Topic_C
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_C --describe
Topic: Topic_C	TopicId: RLFLx0OiQpq3mvVjfMbNTA	PartitionCount: 2	ReplicationFactor: 3	Configs: 
	Topic: Topic_C	Partition: 0	Leader: 3	Replicas: 3,1,2	Isr: 3,1,2
	Topic: Topic_C	Partition: 1	Leader: 1	Replicas: 1,2,3	Isr: 1,2,3
```

The output of the command illustrates the `PartitionCount: 2` and `ReplicationFactor: 3`. It also indicates for each 
partition of the topic, the Broker ID(s) of the Leader, Replicas and In-Sync Replicas (ISR).

### Step 6: List Topics
To display a list of all the Topics within the Kafka Cluster, use the following command:
```shell
# List all the topics on the Kafka Cluster
$ kafka-topics --bootstrap-server localhost:9093 --list
```

### Step 6: Delete Topics
In Apache Kafka, deleting a topic removes all its associated data and metadata from the cluster. While topic deletion 
can be initiated using the Kafka CLI, it's essential to ensure that the broker configuration has `delete.topic.enable` 
set to `true` for the deletion to take effect.

```shell
# Delete the topic called Topic_A
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_A --delete

# Delete the topic called Topic_B
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_B --delete

# Delete the topic called Topic_C
$ kafka-topics --bootstrap-server localhost:9093 --topic Topic_C --delete
```


## Summary
Managing Kafka topics is a foundational aspect of ensuring efficient data streaming and organization within a Kafka 
cluster. The Command Line Interface (CLI) provides an intuitive and direct method to oversee these topics, offering a 
blend of simplicity and power. As we've explored, whether it's topic creation, configuration adjustments, or gaining 
insights, the Kafka Topics CLI is an indispensable tool for administrators and developers alike.

As data streaming continues to be paramount in today's tech landscape, proficiency in tools like the Kafka Topics CLI 
remains invaluable.

Happy streaming!

