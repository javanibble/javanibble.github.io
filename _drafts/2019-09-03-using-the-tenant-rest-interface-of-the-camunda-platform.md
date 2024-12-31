---
layout: post
title: "Using the Tenant REST Interface on the Camunda Platform"
author: andre
categories: [ camunda ]
tags: [camunda, rest-engine, api]
image: /assets/images/feature-images/feature-image-camunda.png
description: This post contains examples of how to use the Tenant REST API of the Camunda BPM engine.
comments: true
related_posts:
  - camunda/_posts/2019-08-31-using-the-user-rest-interface-of-the-camunda-platform.md
  - camunda/_posts/2019-09-01-using-the-group-rest-interface-of-the-camunda-platform.md
---

- Table of Contents
{:toc .large-only}

A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. Camunda BPM also provides a REST API to allow other applications to communicate with it and perform several functions.

This post contains examples of how to use the Tenant REST API of the Camunda BPM engine. There are numerous options in terms of clients you can use like, Postman, Insomnia, and Paw. This post makes use of the curl command to invoke the REST interfaces.


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


### Example 1: Tenant Resource Options 
The **OPTIONS /tenant** and **OPTIONS /tenant/{id}** REST interfaces retrieves the list of available operations that the current authenticated user can perform on the different REST interfaces. See the [documentation][documentation_example1] for more information.

```bash
# Default OPTIONS /tenant command
$ curl -X OPTIONS http://localhost:8080/engine-rest/tenant

# Default OPTIONS /tenant/{ID} command
$ curl -X OPTIONS http://localhost:8080/engine-rest/tenant/knowhere
```


### Example 2: Query List of Tenants
The **GET /tenant** REST interface retrieves a list of tenants or specific tenant based on the id parameter. See the [documentation][documentation_example2] for more information and other parameters you can use. The result is an array of user objects with properties: id and name.

```bash
# Default GET /user REST Interface
$ curl -X GET http://localhost:8080/engine-rest/tenant

# Add parameter *id* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/tenant?id=knowhere'

```


### Example 3: Query the Number of Tenants
The **GET /tenant/count** REST interface queries the number/count of tenants that are configured within the Camunda BPM engine. See the [documentation][documentation_example3] for more information and other parameters you can use.

```bash
# Default GET /tenant/count REST Interface
$ curl -X GET http://localhost:8080/engine-rest/tenant/count

# Add parameter *id* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/tenant/count?id=knowhere'
```


### Example 4: Create a Tenant
The **POST /tenant/create** REST interface creates a new tenant based on the id and name provided as part of the body. See the [documentation][documentation_example4] for more information.

```bash
# Default POST /user/create REST Interface
$ curl -X POST http://localhost:8080/engine-rest/tenant/create \
  -H 'Content-Type: application/json' \
  -d '{
		"id": "knowhere",
		"name": "Knowhere"
	}'
```


### Example 5: Get a Tenant
The **GET /tenant/{id}** REST interface retrieves a specific tenant. See the [documentation][documentation_example5] for more information. The result is an object with properties: id and name. 

```bash
# Default GET /tenant/{id} REST Interface
$ curl -X GET http://localhost:8080/engine-rest/tenant/knowhere
```


### Example 6: Update a Tenant
The **PUT /tenant/{id}** REST interface updates an existing tenant. See the [documentation][documentation_example7] for more information.

```bash
# Default PUT /user/{id}/profile REST Interface
$ curl -X PUT http://localhost:8080/engine-rest/tenant/knowhere \
  -H 'Content-Type: application/json' \
  -d '{
        "id": "knowhere", 
        "name":"Knowhere 2"
    }'
```


### Example 7: Delete a Tenant
The **DELETE /tenant/{id}** REST interface deletes a specific tenant. See the [documentation][documentation_example7] for more information.

```bash
# Default DELETE /tenant/{id} REST Interface
$ curl -X DELETE http://localhost:8080/engine-rest/tenant/knowhere
```


### Example 8: Tenant Group Membership Resource Options
The **OPTIONS /tenant/{id}/group-members** REST interface retrieves the list of available operations that the current authenticated user can perform on the different Tenant Group Membership REST interfaces. See the [documentation][documentation_example8] for more information.

```bash
# Default OPTIONS /tenant/{id}/group-members command
$ curl -X OPTIONS http://localhost:8080/engine-rest/tenant/knowhere/group-members
```


### Example 9: Create a Tenant Group Member
The **PUT /tenant/{id}/group-members/{groupId}** REST interface creates a new membership between the group and the tenant. See the [documentation][documentation_example9] for more information.

```bash
# Default PUT /tenant/{id}/group-members/{groupId} command
$ curl -X PUT http://localhost:8080/engine-rest/tenant/knowhere/group-members/avengers
```


### Example 10: Delete a Tenant Group Member
The **DELETE /tenant/{id}/group-members/{groupId}** REST interface deletes the membership between the group and the tenant. See the [documentation][documentation_example10] for more information.

```bash
# Default DELETE /tenant/{id}/group-members/{groupId} command
$ curl -X DELETE http://localhost:8080/engine-rest/tenant/avengers/group-members/avengers
```

## Summary
Congratulations! You have successfully used the ___Tenant___ REST interface to perform a number of functions on the Camunda BPM engine. Follow me on any of the different social media platforms and feel free to leave comments.



[Install_Postman]:{{site.baseurl}}/how-to-install-postman-on-macos-using-homebrew/
[Install_CURL]:/how-to-install-curl-on-macos-using-homebrew/

[documentation_example1]:https://docs.camunda.org/manual/latest/reference/rest/tenant/options/
[documentation_example2]:https://docs.camunda.org/manual/latest/reference/rest/tenant/get/
[documentation_example3]:https://docs.camunda.org/manual/latest/reference/rest/tenant/get-query-count/
[documentation_example4]:https://docs.camunda.org/manual/latest/reference/rest/tenant/post-create/
[documentation_example5]:https://docs.camunda.org/manual/latest/reference/rest/tenant/get/
[documentation_example6]:https://docs.camunda.org/manual/latest/reference/rest/tenant/put-update/
[documentation_example7]:https://docs.camunda.org/manual/latest/reference/rest/tenant/delete/
[documentation_example8]:https://docs.camunda.org/manual/latest/reference/rest/tenant/group-members/options/
[documentation_example9]:https://docs.camunda.org/manual/latest/reference/rest/tenant/group-members/put/
[documentation_example10]:https://docs.camunda.org/manual/latest/reference/rest/tenant/group-members/delete/
