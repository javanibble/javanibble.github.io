---
layout: post
title: "Implement a BPMN Manual Task in Camunda"
author: andre
categories: [ camunda ]
tags: [camunda, spring boot, bpmn, manual task]
image: /assets/images/feature-images/feature-image-camunda.png
description: The article contains a step-by-step guide on how to implement a BPMN Manual Task in Camunda making use of a Spring Boot Application.
comments: true
related_posts:
  - camunda/_posts/2021-01-03-implement-bpmn-inclusive-gateway-in-camunda.md
  - camunda/_posts/2021-01-04-implement-bpmn-event-based-gateway-in-camunda.md
---

- Table of Contents
{:toc .large-only}

The article contains a step-by-step guide on how to implement a BPMN Manual Task in Camunda making use of a Spring Boot Application. Camunda BPM is an open-source workflow and decision automation platform.

## What is a Manual Task
> “A Manual Task is a Task that is not managed by any business process engine. It can be considered as an unmanaged Task, unmanaged in the sense of that the business process engine doesn’t track the start and completion of such a Task.” [BPMN Specification](https://www.omg.org/spec/BPMN/2.0.2/PDF)

## Getting Started Guide
The following is a step-by-step guide on how to implement a BPMN Manual Task in Camunda making use of a Spring Boot Application. 

### Step 1: Create a Spring Boot Application
Create a spring boot application containing the Camunda BPM Engine. Use the Camunda BPM Initializr website to assist you 
in generating a Spring Boot application. Open the following URL in a browser and complete the form to bootstrap your application.

* [https://start.camunda.com/](https://start.camunda.com/)

Fore a more detailed approach on how to create a spring boot application containing the Camunda BPM Engine, use 
the following link:

* [JavaNibble: Camunda Spring Boot Application](/how-to-create-a-camunda-bpm-spring-boot-application/)

### Step 2: Model the Process
Use Camunda Modeller to model the process. The process model is composed of four manual tasks:

![BPMN Manual Task](/assets/images/posts/bpmn-manual-task/camunda-bpmn-manual-task.png){:.lead width="800" height="100" loading="lazy"}
Example of a manual task
{:.figcaption}

* Retrieve Coffee Order: Is a `Manual Task` linked to an Execution Listener with a Delegate Expressions value of `${executionlistener}`.
* Make Coffee: Is a `Manual Task` linked to an Execution Listener with a Delegate Expressions value of `${executionlistener}`.
* Pour Coffee in Cup: Is a `Manual Task` linked to an Execution Listener with a Delegate Expressions value of `${executionlistener}`.
* Deliver Coffee Order: Is a `Manual Task` linked to an Execution Listener with a Delegate Expressions value of `${executionlistener}`.


### Step 3: Create a ExecutionListener
Implement the `org.camunda.bpm.engine.delegate.ExecutionListener` interface:

```java
@Component("executionlistener")
public class ManualTaskExecutionListener implements ExecutionListener {

    private final Logger LOGGER = LoggerFactory.getLogger(ManualTaskExecutionListener.class.getName());

    public void notify(DelegateExecution delegateExecution) throws Exception {
        LOGGER.info("Manual Task Process: " + delegateExecution.getCurrentActivityName());
    }
}
```

### Step 4: Reference the ExecutionListener from BPMN
The ExecutionListener can be referenced using the `delegateExpression` attribute from the process Engine namespace:

```xml
<bpmn:manualTask id="retrieve-coffee-order" name="Retrieve Coffee Order">
    <bpmn:extensionElements>
        <camunda:executionListener delegateExpression="${executionlistener}" event="start" />
...
<bpmn:manualTask id="make-coffee" name="Make Coffee">
    <bpmn:extensionElements>
        <camunda:executionListener delegateExpression="${executionlistener}" event="start" />
...
<bpmn:manualTask id="pour-coffee-in-cup" name="Pour Coffee in Cup">
    <bpmn:extensionElements>
        <camunda:executionListener delegateExpression="${executionlistener}" event="start" />
...
<bpmn:manualTask id="deliver-coffee-order" name="Deliver Coffee Order">
    <bpmn:extensionElements>
        <camunda:executionListener delegateExpression="${executionlistener}" event="start" />
```

Configure the manual task using the properties panel within the Camunda Modeler.

![Camunda Modeller](/assets/images/posts/bpmn-manual-task/camunda-modeller-bpmn-manual-task.png){:.lead width="800" height="100" loading="lazy"}
Camunda Modeller: Manual Task Properties
{:.figcaption}

### Step 5: View the Spring Boot Application class
The Spring Boot application is implemented by a class called `BasicManualTaskApplication`. The class contains the `@SpringBootApplication` annotation that enables the spring boot auto configuration mechanism, enables the component scan on the packages and allow to register extra beans in the context. 

```java
@SpringBootApplication
public class BasicManualTaskApplication {

    public static void main(String[] args) {
        SpringApplication.run(BasicManualTaskApplication.class);
    }
}
```

### Step 6: Configure the Camunda Spring Boot Application
The properties and configuration of the Spring Boot Application can be found in the `application.yaml` file within the `src/main/resources` folder. To startup your Camunda BPM Spring Boot application, you need to set some properties to allows you access. 

The properties to configure your admin-user are listed below:

```properties
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

The following command instantiates a new instance of the `order-coffee` process.

```shell
$ ./start_process.sh
```

The script performs the following commands:

```shell
curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/order-coffee/start' --header 'Content-Type: application/json'
``` 

The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-manual-task/console-camunda-bpmn-manual-task.png)
Log Statements on Console
{:.figcaption}


## View Camunda Admin Console
To view the Camunda Admin Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

* [http://localhost:8080/](http://localhost:8080/)

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. Type the Username and Password you set within the application properties file.


## View the H2 Console
To view the H2 Console, type the following url in your browser while the application is running. You will be prompted with the login screen.

* [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

After you have typed the above URL in a browser while the application is running, you will be prompted with the login screen. Press the connect button since there is no password specified.

## Example Code
The source code used in this example can be found on [Github](https://github.com/javanibble/camunda-bpmn-manual-task).

## Finally 
Congratulations !!! You have successfully implemented a BPMN Manual Task in Camunda making use of a Spring Boot Application. 

