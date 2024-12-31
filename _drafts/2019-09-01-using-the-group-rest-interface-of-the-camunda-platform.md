---
layout: post
title: "Using the Group REST Interface on the Camunda Platform"
author: andre
categories: [ camunda ]
tags: [camunda, rest-engine, api]
image: /assets/images/feature-images/feature-image-camunda.png
description: This post contains examples of how to use the Group REST API of the Camunda BPM engine.
comments: true
related_posts:
  - camunda/_posts/2019-09-03-using-the-tenant-rest-interface-of-the-camunda-platform.md
  - camunda/_posts/2019-08-31-using-the-user-rest-interface-of-the-camunda-platform.md
---

- Table of Contents
{:toc .large-only}

A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. Camunda BPM also provides a REST API to allow other applications to communicate with it and perform several functions.

This post contains examples of how to use the Group REST API of the Camunda BPM engine. There are numerous options in terms of clients you can use like, Postman, Insomnia, and Paw. This post makes use of the curl command to invoke the REST interfaces.


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


### Example 1: Group Resource Options 
The **OPTIONS /group** and **OPTIONS /group/{id}** REST interfaces retrieves the list of available operations that the current authenticated user can perform on the different Group REST interfaces. See the [documentation][documentation_example1] for more information.

```bash
# Default OPTIONS /group command
$ curl -X OPTIONS http://localhost:8080/engine-rest/group

# Default OPTIONS /group/{ID} command
$ curl -X OPTIONS http://localhost:8080/engine-rest/group/camunda-admin
```


### Example 2: Query List of Groups
The **GET /group** REST interface retrieves a list of groups based on the set of parameters. See the [documentation][documentation_example2] for more information and other parameters you can use. The result is an array of user objects with properties: id, name and type.

```bash
# Default GET /group REST Interface
$ curl -X GET http://localhost:8080/engine-rest/group

# Add parameter *name* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/group?name=Accounting'

# Add parameter *id* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/group?id=camunda-admin'

# Add parameter *type* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/group?type=WORKFLOW'
```


### Example 3: Query the Number of Groups
The **GET /group/count** REST interface queries the number/count of groups that are configured within the Camunda BPM engine. See the [documentation][documentation_example3] for more information and other parameters you can use.

```bash
# Default GET /group/count REST Interface
$ curl -X GET http://localhost:8080/engine-rest/group/count

# Add parameter *type* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/group/count?type=SYSTEM'
```


### Example 4: Create a Group
The **POST /group/create** REST interface creates a new group based on the information provided as part of the body. See the [documentation][documentation_example4] for more information.

```bash
# Default POST /group/create REST Interface
$ curl -X POST http://localhost:8080/engine-rest/group/create \
  -H 'Content-Type: application/json' \
  -d '{
		"id": "avengers",
		"name": "Avengers",
		"type": "WORKFLOW"
	}'
```


### Example 5: Get a Group
The **GET /group/{id}** REST interface retrieves a group by id. See the [documentation][documentation_example5] for more information. The result is a group object with properties: id, name and type. 

```bash
# Default GET /group/{id} REST Interface
$ curl -X GET http://localhost:8080/engine-rest/group/avengers
```


### Example 6: Update a Group
The **PUT /group/{id}** REST interface updates a group associated with a specific id. See the [documentation][documentation_example6] for more information.

```bash
# Default PUT /group/{id} REST Interface
$ curl -X PUT http://localhost:8080/engine-rest/group/avengers \
  -H 'Content-Type: application/json' \
  -d '{
		"id": "avengers",
		"name": "The Avengers",
		"type": "SYSTEM"
	}'
```


### Example 7: Group Membership Resource Options
The **OPTIONS /group/{id}/member** REST interface retrieves the list of available operations that the current authenticated user can perform on the different Group Membership REST interfaces. See the [documentation][documentation_example7] for more information.

```bash
# Default OPTIONS /group/{id}/members command
$ curl -X OPTIONS http://localhost:8080/engine-rest/group/avengers/members
```


### Example 8: Create a Group Member
The **PUT /group/{id}/members/{userId}** REST interface adds a new member to the group based on the information provided as part of the path. See the [documentation][documentation_example8] for more information.

```bash
# Default PUT /group/{id}/members/{userId} command
$ curl -X PUT http://localhost:8080/engine-rest/group/avengers/members/starlord
```


### Example 9: Delete a Group Member
The **DELETE /group/{id}/members/{userId}** REST interface deletes a member of the group based on the information provided as part of the path. See the [documentation][documentation_example9] for more information.

```bash
# Default DELETE /group/{id}/members/{userId} command
$ curl -X DELETE http://localhost:8080/engine-rest/group/avengers/members/starlord
```


### Example 10: Delete a Group
The **DELETE /group/{id}** REST interface deletes the group. See the [documentation][documentation_example10] for more information.

```bash
# Default DELETE /group/{id} REST Interface
$ curl -X DELETE http://localhost:8080/engine-rest/group/avengers
```

## Summary
Congratulations! You have successfully used the ___Group___ REST interface to perform a number of functions on the Camunda BPM engine. Follow me on any of the different social media platforms and feel free to leave comments.



[Install_Postman]:{{site.baseurl}}/how-to-install-postman-on-macos-using-homebrew/
[Install_CURL]:/how-to-install-curl-on-macos-using-homebrew/

[documentation_example1]:https://docs.camunda.org/manual/latest/reference/rest/group/options/
[documentation_example2]:https://docs.camunda.org/manual/latest/reference/rest/group/get-query/
[documentation_example3]:https://docs.camunda.org/manual/latest/reference/rest/group/get-query-count/
[documentation_example4]:https://docs.camunda.org/manual/latest/reference/rest/group/post-create/
[documentation_example5]:https://docs.camunda.org/manual/latest/reference/rest/group/get/
[documentation_example6]:https://docs.camunda.org/manual/latest/reference/rest/group/put-update/
[documentation_example7]:https://docs.camunda.org/manual/latest/reference/rest/group/members/options/
[documentation_example8]:https://docs.camunda.org/manual/latest/reference/rest/group/members/put/
[documentation_example9]:https://docs.camunda.org/manual/latest/reference/rest/group/members/delete/
[documentation_example10]:https://docs.camunda.org/manual/latest/reference/rest/group/delete/

