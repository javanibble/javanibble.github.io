---
layout: post
title: "Using the User REST Interface on the Camunda Platform"
author: andre
categories: [ camunda ]
tags: [camunda, rest-engine, api]
image: /assets/images/feature-images/feature-image-camunda.png
description: This post contains examples of how to use the User REST API of the Camunda BPM engine.
comments: true
related_posts:
  - camunda/_posts/2019-09-03-using-the-tenant-rest-interface-of-the-camunda-platform.md
  - camunda/_posts/2019-09-01-using-the-group-rest-interface-of-the-camunda-platform.md
---

- Table of Contents
{:toc .large-only}

A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. Camunda BPM also provides a REST API to allow other applications to communicate with it and perform several functions.

This post contains examples of how to use the User REST API of the Camunda BPM engine. There are numerous options in terms of clients you can use like, Postman, Insomnia, and Paw. This post makes use of the curl command to invoke the REST interfaces.


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

### Example 1: User Resource Options 
The `OPTIONS /user` and `OPTIONS /user/{id}` REST interfaces retrieves the list of available operations that the current authenticated user can perform on the different REST interfaces. See the [documentation][documentation_example1] for more information.

```bash
# Default OPTIONS /user command
$ curl -X OPTIONS http://localhost:8080/engine-rest/user

# Default OPTIONS /user/{ID} command
$ curl -X OPTIONS http://localhost:8080/engine-rest/user/demo
```


### Example 2: Query List of Users
The **GET /user** REST interface retrieves a list of users based on the set of parameters. See the [documentation][documentation_example2] for more information and other parameters you can use. The result is an array of user objects with properties: id, firstname, lastname and email.

```bash
# Default GET /user REST Interface
$ curl -X GET http://localhost:8080/engine-rest/user

# Add parameter *firstName* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/user?firstName=Demo'

# Add parameter *id* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/user?id=john'

# Add parameter *memberOfGroup* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/user?memberOfGroup=camunda-admin'
```


### Example 3: Query the Number of Users
The **GET /user/count** REST interface queries the number/count of users that are configured within the Camunda BPM engine. See the [documentation][documentation_example3] for more information and other parameters you can use.

```bash
# Default GET /user/count REST Interface
$ curl -X GET http://localhost:8080/engine-rest/user/count

# Add parameter *firstName* to REST Interface
$ curl -X GET 'http://localhost:8080/engine-rest/user/count?firstName=Demo'
```


### Example 4: Create a User
The **POST /user/create** REST interface creates a new user based on the profile and credentials provided as part of the body. See the [documentation][documentation_example4] for more information.

```bash
# Default POST /user/create REST Interface
$ curl -X POST http://localhost:8080/engine-rest/user/create \
  -H 'Content-Type: application/json' \
  -d '{
	"profile": {
		"id": "starlord",
		"firstName": "Peter",
		"lastName": "Quill",
		"email": "starlord@avengers.com"
	},
	"credentials": {
		"password": "guardian"
	}
}'
```


### Example 5: Get a User's Profile
The **GET /user/{id}/profile** REST interface retrieves the profile of the user. See the [documentation][documentation_example5] for more information. The result is an array of user objects with properties: id, firstname, lastname, email and links. 

```bash
# Default GET /user/{id}/profile REST Interface
$ curl -X GET http://localhost:8080/engine-rest/user/starlord/profile
```


### Example 6: Unlock a User
The **GET /user/{id}/unlock** REST interface unlocks the user. See the [documentation][documentation_example6] for more information.

```bash
# Default GET /user/{id}/unlock REST Interface
$ curl -X GET http://localhost:8080/engine-rest/user/starlord/unlock
```


### Example 7: Update a User's Profile
The **PUT /user/{id}/profile** REST interface updates the profile of an existing user. See the [documentation][documentation_example7] for more information.

```bash
# Default PUT /user/{id}/profile REST Interface
$ curl -X PUT http://localhost:8080/engine-rest/user/starlord/profile \
  -H 'Content-Type: application/json' \
  -d '{
        "id": "starlord", 
        "firstName":"New_Peter", 
        "lastName":"New_Quill", 
        "email":"new_starlord@avengers.com" 
    }'
```


### Example 8: Update a User's Credentials
The **PUT /user/{id}/credentials** REST interface update the credentials of an existing user. See the [documentation][documentation_example8] for more information.

```bash
# Default PUT /user/{id}/credentials REST Interface
$ curl -X PUT http://localhost:8080/engine-rest/user/starlord/credentials \
  -H 'Content-Type: application/json' \
  -d '{
        "password":"updated_password", 
        "authenticatedUserPassword":"ROOT" 
    }'
```

### Example 9: Delete a User
The **DELETE /user/{id}** REST interface deletes the user. See the [documentation][documentation_example9] for more information.

```bash
# Default DELETE /user/{id} REST Interface
$ curl -X DELETE http://localhost:8080/engine-rest/user/starlord
```

## Summary
Congratulations! You have successfully used the ___User___ REST interface to perform a number of functions on the Camunda BPM engine. Follow me on any of the different social media platforms and feel free to leave comments.



[Install_Docker]:/how-to-install-docker-on-macos-using-homebrew/
[Install_CURL]:/how-to-install-curl-on-macos-using-homebrew/

[documentation_example1]:https://docs.camunda.org/manual/latest/reference/rest/user/options/
[documentation_example2]:https://docs.camunda.org/manual/latest/reference/rest/user/get-query/
[documentation_example3]:https://docs.camunda.org/manual/latest/reference/rest/user/get-query-count/
[documentation_example4]:https://docs.camunda.org/manual/latest/reference/rest/user/post-create/
[documentation_example5]:https://docs.camunda.org/manual/latest/reference/rest/user/get/
[documentation_example6]:https://docs.camunda.org/manual/latest/reference/rest/user/unlock/
[documentation_example7]:https://docs.camunda.org/manual/latest/reference/rest/user/put-update-profile/
[documentation_example8]:https://docs.camunda.org/manual/latest/reference/rest/user/put-update-credentials/
[documentation_example9]:https://docs.camunda.org/manual/latest/reference/rest/user/delete/