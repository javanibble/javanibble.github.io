---
layout: post
title: "Implement a BPMN Event-based Gateway in Camunda"
author: andre
categories: [ camunda ]
tags: [camunda, spring boot, bpmn, event-based gateway]
image: /assets/images/feature-images/feature-image-camunda.png
description: The article contains a step-by-step guide on how to implement a BPMN Event-based Gateway in Camunda making use of a Spring Boot Application.
comments: true
related_posts:
  - camunda/_posts/2021-01-05-implement-bpmn-parallel-gateway-in-camunda.md
  - camunda/_posts/2021-01-06-implement-bpmn-manual-task-in-camunda.md
---

- Table of Contents
{:toc .large-only}

The article contains a step-by-step guide on how to implement a BPMN Event-based Gateway in Camunda making use of a Spring Boot Application. Camunda BPM is an open-source workflow and decision automation platform.

## What is an Event-based Gateway
> “The Event-Based Gateway represents a branching point in the Process where the alternative paths that follow the Gateway are based on Events that occur, rather than the evaluation of Expressions using Process data. A specific Event, usually the receipt of a Message, determines the path that will be taken. Basically, the decision is made by another Participant, based on data that is not visible to Process, thus, requiring the use of the Event-Based Gateway.” ~ BPMN Event-based Gateway

## Getting Started Guide
The following is a step-by-step guide on how to implement a BPMN Event-based Gateway in Camunda making use of a Spring Boot Application. 

### Step 1: Create a Spring Boot Application
Create a spring boot application containing the Camunda BPM Engine. Use the Camunda BPM Initializr website to assist you 
in generating a Spring Boot application. Open the following URL in a browser and complete the form to bootstrap your application.

* [https://start.camunda.com/](https://start.camunda.com/)

Fore a more detailed approach on how to create a spring boot application containing the Camunda BPM Engine, use 
the following link:

* [JavaNibble: Camunda Spring Boot Application](/how-to-create-a-camunda-bpm-spring-boot-application/)

### Step 2: Model the Process
Use Camunda Modeller to model the process. The process model is composed of four tasks, an event-based gateway, timer event and two message events:

![BPMN Event-based Gateway](/assets/images/posts/bpmn-event-based-gateway/bpmn-event-based-gateway.png){:.lead width="800" height="100" loading="lazy"}
Example of an event-based gateway
{:.figcaption}

* Submit Payment Request: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Payment Event: Is an `Event-based Gateway` with three sequence flows.
* 2 min Timeout: Is a `Timer Event` with a duration of `PT1M`.
* Payment Failed: Is a `Message Event` with a message name of `payment-failed-message`.
* Payment Successful: Is a `Message Event` with a message name of `payment-successful-message`.
* Submit Timeout Reversal: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Print Payment Failure Receipt: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Print Payment Receipt: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.

### Step 3: Create a Java Delegate
Implement the `org.camunda.bpm.engine.delegate.JavaDelegate` interface:

```java
@Component("logger")
public class ConsoleLoggerDelegate implements JavaDelegate {

    private final Logger LOGGER = LoggerFactory.getLogger(ConsoleLoggerDelegate.class.getName());

    public void execute(DelegateExecution execution) throws Exception {
        LOGGER.info("Place Order Process: " + execution.getCurrentActivityName());
    }
}
```

### Step 4: Reference the JavaDelegate from BPMN
The JavaDelegate can be referenced using the `delegateExpression` attribute from the process Engine namespace:

```xml
<bpmn:serviceTask id="submit-payment-request" name="Submit Payment Request" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="submit-timeout-reversal" name="Submit Timeout Reversal" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="print-payment-failure-receipt" name="Print Payment Failure Receipt" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="print-payment-receipt" name="Print Payment Receipt" camunda:delegateExpression="${logger}">
...
```

Configure the service task using the properties panel wihtin the Camunda Modeler.

![Camunda Modeller](/assets/images/posts/bpmn-event-based-gateway/camunda-modeller-bpmn-event-based-gateway.png){:.lead width="800" height="100" loading="lazy"}
Camunda Modeller: Service Task Properties
{:.figcaption}

### Step 5: View the Spring Boot Application class
The Spring Boot application is implemented by a class called `BasicEventBasedGatewayApplication`. The class contains the `@SpringBootApplication` annotation that enables the spring boot auto configuration mechanism, enables the component scan on the packages and allow to register extra beans in the context. 

```java
@SpringBootApplication
public class BasicEventBasedGatewayApplication {
  public static void main(String[] args) {
    SpringApplication.run(BasicEventBasedGatewayApplication.class);
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

**Run the command: Scenario 1 - Timeout**

Scenario 1 is starting the Payment process and passing in the `businesskey` with a value of `business-key-123`. The event-based gateway waits for either the timer event to occur, or one of the two message events.

After two minutes the timer event is triggered and the payment is reversed. 

```shell
$ ./start_process_scenario_01.sh
```
The script performs the following commands:

```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/payment-process/start' --header 'Content-Type: application/json' --data-raw '{
       "businessKey": "business-key-123"
  }'
```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-event-based-gateway/console-camunda-bpmn-event-based-gateway-scenario1.png)
Log Statements on Console
{:.figcaption}


**Run the command: Scenario 2 - Payment Failed**

Scenario 2 is starting the Payment process and passing in the `businesskey` with a value of `business-key-123`. The event-based gateway waits for either the timer event to occur, or one of the two message events.

A `payment-failed-message` message is sent to the process instance with `businesskey` of value `business-key-123` to indicate the payment has failed.

```shell
$ ./start_process_scenario_02.sh
```
The script performs the following commands:

```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/payment-process/start' --header 'Content-Type: application/json' --data-raw '{
     "businessKey": "business-key-123"
}'

sleep 5

$ curl --location --request POST 'http://localhost:8080/engine-rest/message' --header 'Content-Type: application/json' --data-raw '{
     "messageName": "payment-failed-message",
     "businessKey": "business-key-123"
}'

```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-event-based-gateway/console-camunda-bpmn-event-based-gateway-scenario2.png)
Log Statements on Console
{:.figcaption}

**Run the command: Scenario 3 - Payment Successful**

Scenario 2 is starting the Payment process and passing in the `businesskey` with a value of `business-key-123`. The event-based gateway waits for either the timer event to occur, or one of the two message events.

A `payment-successful-message` message is sent to the process instance with `businesskey` of value `business-key-123` to indicate the payment was successful.

```shell
$ ./start_process_scenario_03.sh
```
The script performs the following commands:

```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/payment-process/start' --header 'Content-Type: application/json' --data-raw '{
     "businessKey": "business-key-123"
}'

sleep 5

$ curl --location --request POST 'http://localhost:8080/engine-rest/message' --header 'Content-Type: application/json' --data-raw '{
     "messageName": "payment-successful-message",
     "businessKey": "business-key-123"
}'
```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-event-based-gateway/console-camunda-bpmn-event-based-gateway-scenario3.png)
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
The source code used in this example can be found on [Github](https://github.com/javanibble/camunda-bpmn-event-based-gateway).

## Finally 
Congratulations !!! You have successfully implemented a BPMN Event-based Gateway in Camunda making use of a Spring Boot Application. 
