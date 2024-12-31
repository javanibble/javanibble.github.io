---
layout: post
title: "How to configure AWS CLI"
author: andre
categories: [ aws ]
tags: [aws cli, aws]
image: /assets/images/feature-images/feature-image-aws.png
description: This article provides a set of commands on how to configure Amazon Web Services Command Line Interface (AWS CLI) on macOS or any other operating system.
comments: true
---

- Table of Contents
{:toc .large-only}

This article provides a set of commands on how to configure Amazon Web Services Command Line Interface (AWS CLI) on macOS or any other operating system. The AWS CLI is an open source tool that enables the user of the AWS platform to communicate and issue commands to AWS Services.

## Requirements
The following list defines the technologies, tools and credentials required to configure the AWS CLI tool:

* AWS Account & Credentials.
* Installed AWS CLI tool. ([AWS CLI on macOS][1])
* iTerm or Terminal. ([iTerm2 on macOS][2])

## What is AWS CLI?
AWS CLI is an open source tool that enables AWS Platform users to communicate and issue commands to their services. The command line tool enables users to invoke the AWS Platform services via the different public APIs. The authentication and other security mechanisms are abstracted away from the user by configuring the AWS CLI with he user's access key and secret. Furthermore, it provides higher level operations by combining the finer grained public APIs of the AWS Services into simple operations. These higher level operations will be more natural to use for a user. Users can now manage their AWS Services by creating shell scripts and automate simple and complex tasks alike.

## Quick Commands
This section provides the command on how to configure AWS CLI.
```bash
$ aws configure
AWS Access Key ID [****************OMLQ]: ********
AWS Secret Access Key [****************BQWW]: ***********
Default region name [us-east-1]: eu-west-1
Default output format [json]: json
```

**Default Region**: For a list of available regions, see [AWS Regions and Endpoints][3]. 

**Default Output**: The default output format can be either *json*, *text*, or *table*.

## AWS Configuration Files
### AWS Credential file
The AWS Credential file contains the credentials of multiple named profiles including the default profile. The credentials of each profile consist of the key/values for the `aws_access_key_id` and `aws_secret_access_key` properties. The AWS credentials file is located at `~/.aws/credentials` on macOS. 
```bash
$ cat ~/.aws/credentials
[default]
aws_access_key_id=1234567890
aws_secret_access_key=ABCDEFGHIJKLMNOPQRSTUVWXYZ

[user2]
aws_access_key_id=0987654321
aws_secret_access_key=ZYXWVUTSRQPONMLKJIHGFEDCBA
```

### CLI Configuration file
The CLI Configuration file contains the configuration of multiple named profiles including the default profile. The configuration of each profile consist of the key/values for the `region` and `output` properties. The AWS CLI configuration file is located at `~/.aws/config` on macOS. 
```bash
$ cat ~/.aws/config
[default]
region=us-west-2
output=json

[profile user2]
region=us-east-1
output=text
```

## AWS Configure Commands
The following are additional commands that can be used during the configuration of the AWS CLI tool.
### 1. AWS Configure a Named Profile
You can configure a named pro-file using the `--profile` argument as part of the AWS Configure command.
```bash
$ aws configure --profile administrator
AWS Access Key ID [None]: 12334567890
AWS Secret Access Key [None]: ABCDEFGHIJKLMNOPQRSTUVWXYZ
Default region name [None]: eu-west-1
Default output format [None]: json
```

**Note:** The named profile argument `--profile` can be appended to any of the AWS Configure commands to execute the command in context of that named profile.  

### 2. Update a Specific Property
You can run the AWS Configure command multiple times to update specific properties. To existing value is displayed in [brackets]. To update the existing value, type a new value and press enter. To keep an existing value, press enter without typing any value in.
```bash
$ aws configure
AWS Access Key ID [****************1234]: 
AWS Secret Access Key [****************1234]: 
Default region name [eu-west-1]: 
Default output format [json]: table
```

### 3. List Config Data
The following command can be used to list the AWS CLI Configuration data of the default profile. For each configuration item, it will  show you  the  value,  where  the configuration value was retrieved, and the configuration variable name.
```bash
$ aws configure list
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key     ****************1234 shared-credentials-file    
secret_key     ****************1234 shared-credentials-file    
    region                eu-west-1      config-file    ~/.aws/config
```

## Finally
Congratulations! You have successfully configured AWS CLI and will now be able to issue commands to the AWS Platform. 

[1]:https://www.javanibble.com/how-to-install-awscli-on-macos-using-homebrew/
[2]:https://www.javanibble.com/how-to-install-iterm2-on-macos-using-homebrew/
[3]:https://docs.aws.amazon.com/general/latest/gr/rande.html