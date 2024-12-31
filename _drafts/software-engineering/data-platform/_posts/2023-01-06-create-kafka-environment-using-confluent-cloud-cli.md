---
layout: post
title: "Create a Kafka Environment using Confluent Cloud and CLI"
author: andre
categories: [ software-engineering, data-platform ]
tags: [apache-kafka]
image: /assets/images/feature-images/feature-image-kafka.jpg
description: A step-by-step guide using the Confluent CLI to create a Confluent Kafka Cluster on different cloud platforms.
comments: true
---

- Table of Contents
{:toc .large-only}

This guide aims to provide you with a step-by-step process to set up a Kafka environment using Confluent Cloud. You will learn to install the Confluent CLI with Homebrew and create your Kafka cluster on major cloud platforms such as AWS, Azure, and Google Cloud.

This introduction will help you experience a hassle-free setup, enabling you to unleash the full potential of Kafka without the complexities of manual configuration. Whether you are an experienced developer or a beginner, this guide will assist you in efficiently and effectively using Kafka in the cloud.

## Step 1: Sign Up for a Confluent Cloud Account
First sign up for a free [Confluent Cloud](https://www.confluent.io/get-started/) account. After you have registered and
created your Confluent account, you can log into your account here: [Confluent Cloud](https://www.confluent.io/).

Note: Get $100 of free usage with the promo code `100DAYSKAFKA`. This can be applied in the Billing & Payment section of
your account.

## Step 2: Setup Confluent CLI
The setup of the Confluent CLI begins with its installation, a straightforward process that integrates seamlessly into 
your existing system. Once installed, you simply use your Confluent account credentials to log in through the CLI, 
establishing a secure and personalised connection to Confluent’s services.

For alternative options or a more detailed solution, please refer to the Confluent CLI documentation for more details.

**Command**: _Install Confluent CLI_
```shell
$ brew install confluent-cl
```

**Command**: _Log Into Confluent Cloud account_
To access Confluent Cloud, log in using your email and password, ensuring a secure entry into the platform. For added 
convenience, your email and password can be stored locally with the `--save` flag, enabling non-interactive 
re-authentication for future sessions.

```shell
$ confluent login --prompt --save
```
You will be prompted for your email and password and logged in for the default organisation you have created.

## Step 3: Create a Kafka Cluster
Creating a Kafka cluster is done using the `confluent kafka cluster create` command, where specifying the cloud 
provider (`aws`, `azure`, or `gcp`) and the respective cloud region ID is mandatory, ensuring the cluster is set up in 
your desired cloud environment.

```shell
# Use the following template 
# confluent kafka cluster create <name> --cloud <provider> --region <region>
# Create Kafka Cluster called my_first_cluster on AWS in the us-east-1 region.
$ confluent kafka cluster create my_first_cluster --cloud aws --region us-east-1
```

It takes a few minutes for the cluster to be created and provisioned. Use the following command to determine if the cluster is available.

```shell
$ confluent kafka cluster list
```

It is important to set the created cluster as the active cluster. Setting the Kafka cluster as the default streamlines operations by automatically directing commands to it, saving time and reducing errors in environments with multiple clusters.

```shell
# Replace the <cluster ID> with the ID listed as part of the list command.
$ confluent kafka cluster use <cluster ID>
```

## Step 4: Create a Kafka Topic
Creating a Kafka topic is accomplished using the `confluent kafka topic create <topic> [flags]` command, allowing for 
customised topic configuration through various optional flags.

```shell
# Create a Kafka topic with the name my_first_topic
$ confluent kafka topic create my_first_topic --partitions 1
```

## Step 5: Create an API Key
Confluent API keys are used for authentication and authorisation purposes, providing secure access to Confluent Cloud 
services. They enable clients to produce and consume messages from Kafka clusters and interact with other Confluent 
Cloud resources, ensuring that these interactions are both secure and restricted to authorised users and applications.

These keys play a critical role in managing access control in distributed systems, maintaining the integrity and 
security of data flows within Kafka environments.

```shell
# Replace the <cluster ID> with the ID listed as part of the list command.
$ confluent api-key create --resource <cluster ID>
```

Set the API Key as the active API key to be used in subsequent commands which support passing an API key with the 
`--api-key` flag.

```shell
# Replace the <API Key> and <cluster ID> with values from previous commands.
$ confluent api-key use <API key> --resource <cluster ID>
```

## Step 6: Produce a Message
Starting a Kafka producer is executed with the `confluent kafka topic produce <topic_name>` command, enabling the 
sending of messages to a specified Kafka topic. Use `Ctrl-C` or `Ctrl-D` to exit.

```shell
$ confluent kafka topic produce my_first_topic
> Hello 1
> Hello 2
> Hello 3
> ^C
```

## Step 7: Consume a Message
Starting a Kafka consumer is streamlined with the `confluent kafka topic consume` command, and by using the 
`--from-beginning` flag, you can retrieve messages from the very start of the topic, ensuring no data is missed from the 
time the topic was created. Use `Ctrl-C` or `Ctrl-D` to exit.

```shell
$ confluent kafka topic consume my_first_topic --from-beginning
Hello 1
Hello 2
Hello 3
> ^C
```

## Step 8: Delete API Key
To delete a Confluent API key, use the `confluent api-key delete <API key>` command, which effectively removes the 
specified key from your Confluent environment. This action ensures that the key is no longer active or usable for 
authentication, enhancing the security and management of your Kafka configurations.

```shell
$ confluent api-key delete <API key>
```

## Step 9: Delete Kafka Topic
Deleting a Kafka topic in your Confluent environment is straight forward with the `confluent kafka topic delete <name>` 
command, where you specify the exact name of the topic you want to remove.

```shell
$ confluent kafka topic delete my_first_topic
```

## Step 10: Delete Kafka Cluster
To remove a Kafka cluster from your Confluent environment, you can use the `confluent kafka cluster delete <Cluster ID>` 
command, specifying the unique ID of the cluster you wish to delete. This command permanently deletes the specified 
Kafka cluster, terminating all associated services and data storage within that cluster.

```shell
# Replace the <cluster ID> with the ID listed as part of the list command.
$ confluent kafka cluster delete <cluster ID>
```

## Summary
Finally, creating a Kafka environment using Confluent Cloud represents a streamlined, efficient approach for both beginners and experienced users. This guide demonstrated the ease of installing the Confluent CLI via Homebrew, creating an account with Confluent, and setting up a Kafka cluster on your choice of cloud provider — AWS, Azure, or Google Cloud.

Happy streaming!
