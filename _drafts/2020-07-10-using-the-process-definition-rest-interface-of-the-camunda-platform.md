---
layout: post
title: "Using the Process-Definition REST Interface on the Camunda Platform"
author: andre
categories: [ camunda ]
tags: [camunda, rest-engine, api]
image: /assets/images/feature-images/feature-image-camunda.png
description: This post contains examples of how to use the Process Definition REST API of the Camunda BPM engine.
comments: true
related_posts:
  - camunda/_posts/2019-08-31-using-the-user-rest-interface-of-the-camunda-platform.md
  - camunda/_posts/2019-09-01-using-the-group-rest-interface-of-the-camunda-platform.md
---

- Table of Contents
{:toc .large-only}

A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. Camunda BPM also provides a REST API to allow other applications to communicate with it and perform several functions.

This post contains examples of how to use the Process Definition REST API of the Camunda BPM engine. There are numerous options in terms of clients you can use like, Postman, Insomnia, and Paw. This post makes use of the curl command to invoke the REST interfaces.


## Getting Started
The following list defines the technologies and libraries I used to implement the sample code:

* [Docker][Install_Docker]
* [curl][Install_CURL]


## Start Camunda BPM Platform
The following commands are all you need to get a docker container with the Camunda BPM Platform running. The command also defines the container name and the port to expose on the host.

```shell
# Creates a container layer over the camunda bpm platform image and then starts it.
$ docker run -d --name camunda -p 8080:8080 camunda/camunda-bpm-platform:latest

# Fetches the logs of the container.
$ docker logs -f camunda
```

After your Camunda BPM Platform is up and running, you can open the Camunda Admin web application by navigating to the following url in your browser:

```url
http://localhost:8080/camunda-welcome/index.html
# Username: demo
# Password: demo
```

The REST API is available on the following URL:
```url
http://localhost:8080/engine-rest
```


### Example 1: Start a Instance
The `OPTIONS /user` and `OPTIONS /user/{id}` REST interfaces retrieves the list of available operations that the current authenticated user can perform on the different REST interfaces. See the [documentation][documentation_example1] for more information.

```bash
# Default OPTIONS /user command
$ curl -X POST 'http://localhost:8080/engine-rest/process-definition/key/invoice/start' \
-H 'Content-Type: application/json' \
-d '{
    "variables": {
        "mypath": {
            "value": 2,
            "type": "Integer"
        }
    }
}'
```


## Summary
Congratulations! You have successfully used the `process-definition` REST interface to perform a number of functions on the Camunda BPM engine. Follow me on any of the different social media platforms and feel free to leave comments.


[Install_Postman]:{{site.baseurl}}/how-to-install-postman-on-macos-using-homebrew/
[Install_CURL]:/how-to-install-curl-on-macos-using-homebrew/

[documentation_example1]:https://docs.camunda.org/manual/latest/reference/rest/process-definition/post-start-process-instance/
