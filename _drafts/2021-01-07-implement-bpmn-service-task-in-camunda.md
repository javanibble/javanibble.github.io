---
layout: post
title: "Implement a BPMN Service Task in Camunda"
author: andre
categories: [ camunda ]
tags: [camunda, spring boot, bpmn, service task]
image: /assets/images/feature-images/feature-image-camunda.png
description: The article contains a step-by-step guide on how to implement a BPMN Service Task in Camunda making use of a Spring Boot Application.
comments: true
related_posts:
  - camunda/_posts/2021-01-06-implement-bpmn-manual-task-in-camunda.md
  - camunda/_posts/2021-01-04-implement-bpmn-event-based-gateway-in-camunda.md
---

- Table of Contents
{:toc .large-only}

The article contains a step-by-step guide on how to implement a BPMN Service Task in Camunda making use of a Spring Boot Application. A Service Task within Camunda is used to either invoke Java code or to place a work item within a topic for an external worker to retrieve asynchronously.

## What is a Service Task
> “A Service Task is a Task that uses some sort of service, which could be a Web service or an automated application. A Service Task object shares the same shape as the Task, which is a rectangle that has rounded corners. However, there is a graphical marker in the upper left corner of the shape that indicates that the Task is a Service Task” [BPMN Specification](https://www.omg.org/spec/BPMN/2.0.2/PDF)

## Getting Started Guide
The following is a step-by-step guide on how to implement a BPMN Service Task in Camunda making use of a Spring Boot Application. 

### Step 1: Create a Spring Boot Application
Create a spring boot application containing the Camunda BPM Engine. Use the Camunda BPM Initializr website to assist you 
in generating a Spring Boot application. Open the following URL in a browser and complete the form to bootstrap your application.

* [https://start.camunda.com/](https://start.camunda.com/)

For a more detailed approach on how to create a spring boot application containing the Camunda BPM Engine, use the 
following link:

* [JavaNibble: Camunda Spring Boot Application](/how-to-create-a-camunda-bpm-spring-boot-application/)

### Step 2: Model the Process
Camunda provides two ways for a service task to invoke services, namely Invoking Java Code and External Tasks. The above
business process shows how to invoke services making use of several ways. The process engine invokes the java code
synchronously except for the external tasks, where the process engine creates a work item and places it within a topic.
External workers poll the process engine based on a topic and retrieve the work items.

Use Camunda Modeller to model the process. The process model composes of four service tasks:

![BPMN Service Task](/assets/images/posts/bpmn-service-task/bpmn-service-task.png){:.lead width="800" height="100" loading="lazy"}
Example of a service task
{:.figcaption}

* Retrieve Coffee Order: Is a `Service Task` using `Java Class` as implementation and `com.javanibble.camunda.examples.RetrieveCoffeeOrderDelegate` as the Java Class.
* Make Coffee: Is a `Service Task` using `Delegate Expressions` as implementation and value of `${makeCoffee}`.
* Pour Coffee in Cup: Is a `Service Task` using `Expression` as implementation and value of `${coffeeService.pourCoffee(execution)}`.
* Deliver Coffee Order: Is a `Service Task` using `External` as implementation and topic value of `deliverCoffeeOrder`.

The BPMN source code used in this example is available on [GitHub](https://github.com/javanibble/camunda-bpmn-service-task/blob/master/src/main/resources/bpmn-service-task.bpmn).

### Step 3 Invoke Java Code: Java Class
The "Retrieve Coffee Order" service task specifies a java class that implements a `JavaDelegate` interface. The Java class will be
called during the process execution and hence the fully qualified name is required.

```xml
<bpmn:serviceTask id="retrieve-coffee-order" name="Retrieve Coffee Order" 
                  camunda:class="com.javanibble.camunda.examples.RetrieveCoffeeOrderDelegate">
```
**Java Code:**

Create a Java class `RetrieveCoffeeOrderDelegate` that implements the `org.camunda.bpm.engine.delegate.JavaDelegate` interface.

```java
package com.javanibble.camunda.examples;

public class RetrieveCoffeeOrderDelegate implements JavaDelegate {

    private final Logger LOGGER = LoggerFactory.getLogger(RetrieveCoffeeOrderDelegate.class.getName());

    public void execute(DelegateExecution execution) throws Exception {
        String coffeeOrder = (String) execution.getVariable("order");

        LOGGER.info("Order Coffee Process: " + execution.getCurrentActivityName() + " - " + coffeeOrder);
    }

}
```

### Step 4: Invoke Java Code: Delegate Expression
The "Make Coffee" service task makes use of a Delegate Expression that resolves to a specific object. This object must 
follow the same rules as objects that are created when the camunda:class attribute is used.
```xml
<bpmn:serviceTask id="make-coffee" name="Make Coffee" 
                  camunda:delegateExpression="${makeCoffee}">
```
**Java Code:**

Create a Java class `MakeCoffeeDelegate` that implements the `org.camunda.bpm.engine.delegate.JavaDelegate` interface.

```java
@Component("makeCoffee")
public class MakeCoffeeDelegate implements JavaDelegate {

    private final Logger LOGGER = LoggerFactory.getLogger(RetrieveCoffeeOrderDelegate.class.getName());

    public void execute(DelegateExecution execution) throws Exception {
        String coffeeOrder = (String) execution.getVariable("order");

        LOGGER.info("Order Coffee Process: " + execution.getCurrentActivityName() + " - " + coffeeOrder);
    }
}
```


### Step 5: Invoke Java Code: Expression
The "Pour Coffee in Cup" service task makes use of an expression which calls a method.
```xml
<bpmn:serviceTask id="pour-coffee-in-cup" name="Pour Coffee in Cup" 
                  camunda:expression="${coffeeService.pourCoffee(execution)}">
```
**Java Code:**

Create a Java class `CoffeeService` and a method called `pourCoffee` that uses a `DelegateExecution` as a parameter.

```java
@Component
public class CoffeeService {

    private final Logger LOGGER = LoggerFactory.getLogger(RetrieveCoffeeOrderDelegate.class.getName());

    public void pourCoffee(DelegateExecution execution) throws Exception {
        String coffeeOrder = (String) execution.getVariable("order");

        LOGGER.info("Order Coffee Process: " + execution.getCurrentActivityName() + " - " + coffeeOrder);
    }
}
```


### Step 6: External Task
The "Deliver Coffee Order" service task is handled externally as an external task. The `camunda:type` attribute is set to
`external` and the `camunda:topic` attribute specifies the external tasks' topic.
```xml
<bpmn:serviceTask id="deliver-coffee-order"  name="Deliver Coffee Order" 
                  camunda:type="external" camunda:topic="deliverCoffeeOrder">
```

There are several ways for external tasks to be implemented, but this example will use the REST APIs to `fectAndLock` and 
`complete` the external tasks. 

**Fetch & Lock External Task**

Fetches and locks a specific number of external tasks for execution by a worker. Query can be restricted to specific task topics and for each task topic an individual lock time can be provided.

```shell
$ curl --location --fail --silent --request POST 'http://localhost:8080/engine-rest/external-task/fetchAndLock' --header 'Content-Type: application/json' --data-raw '{"workerId":"aWorkerId","maxTasks":1,"usePriority":true,"topics":[{"topicName": "deliverCoffeeOrder","lockDuration": 10000,"variables": ["orderId"]}]}'
```

**Complete External Task**

Completes an external task by id and updates process variables.

```shell
$ curl --location --fail --silent --request POST "http://localhost:8080/engine-rest/external-task/$TASK_ID/complete" --header 'Content-Type: application/json' --data-raw '{"workerId": "aWorkerId","variables":{},"localVariables":{}}'
```

### Step 7: Create the Spring Boot Application class
The Spring Boot application is implemented by a class called `BasicServiceTaskApplication`. The class contains the `@SpringBootApplication` annotation that enables the spring boot auto configuration mechanism, enables the component scan on the packages and allow to register extra beans in the context. 

```java
@SpringBootApplication
public class BasicServiceTaskApplication {

    public static void main(String[] args) {
        SpringApplication.run(BasicServiceTaskApplication.class);
    }

}
```

### Step 8: Configure the Camunda Spring Boot Application
The properties and configuration of the Spring Boot Application can be found in the `application.yaml` file within the `src/main/resources` folder. To startup your Camunda BPM Spring Boot application, you need to set some properties to allows you access. 

The properties to configure your admin-user are listed below:

```yaml
spring.datasource.url: jdbc:h2:mem:camunda-h2-database;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE

camunda.bpm.admin-user:
  id: demo
  password: demo

spring.h2.console:
  enabled: true
  path: /h2-console
```


## Compile & Run The Example
### 1. Compile the application
Use the following command to compile the Spring Boot application making use of maven:

```shell
$ mvn clean install
```

### 2. Run the application
After you have successfully built the Camunda BPM Spring Boot application, the compiled artifact can be found in the
target directory. Use the following command to start the Camunda BPM Spring Boot Application.

```shell
$ mvn spring-boot:run
```

### 3. Execute the example
After the application has started, run the following command in another terminal:

**Run the command: Start Process Instance**

The following command instantiates a new instance of the `order-coffee` process and pass the process variable called
`order` with a value of `Espresso` to the process engine as part of the request body.

```shell
$ ./start_process.sh
```
The script performs the following commands:
```shell
curl --location --silent --output --request POST 'http://localhost:8080/engine-rest/process-definition/key/order-coffee/start' --header 'Content-Type: application/json' --data-raw '{
     "variables": {
         "order": {
             "value": "Espresso",
             "type": "String"
        }
    }
}'
```

The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-service-task/console-camunda-bpmn-service-task.png)
Log Statements on Console
{:.figcaption}

**Run the command: External Task**

The following script is used to fetchAndLock the external task and then after 2 seconds, the external task is completed.

```shell
$ ./run_external_task.sh
```
The script performs the following commands:
```shell
echo "\nDeliver Coffee Order Task: Fetch & Lock External Task"
TASK_ID=$(curl --location --fail --silent --request POST 'http://localhost:8080/engine-rest/external-task/fetchAndLock' --header 'Content-Type: application/json' --data-raw '{"workerId":"aWorkerId","maxTasks":1,"usePriority":true,"topics":[{"topicName": "deliverCoffeeOrder","lockDuration": 10000,"variables": ["orderId"]}]}' | jq -r '.[0].id')

sleep 2
echo "\nDeliver Coffee Order Task: Complete External Task"
curl --location --fail --silent --request POST "http://localhost:8080/engine-rest/external-task/$TASK_ID/complete" --header 'Content-Type: application/json' --data-raw '{"workerId": "aWorkerId","variables":{},"localVariables":{}}'
```

## View Camunda Admin Console
To view the Camunda Admin Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

* [http://localhost:8080/](http://localhost:8080/)

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. Type the Username and Password you set within the application properties file.


## View the H2 Console
To view the H2 Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

* [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. Press the connect button since there is no password specified.

## Example Code
The source code used in this example can be found on [Github](https://github.com/javanibble/camunda-bpmn-service-task).

## Finally 
Congratulations !!! You have successfully implemented a BPMN Service Task in Camunda making use of a Spring Boot Application. 

