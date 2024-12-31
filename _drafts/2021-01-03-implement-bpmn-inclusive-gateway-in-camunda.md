---
layout: post
title: "Implement a BPMN Inclusive Gateway in Camunda"
author: andre
categories: [ camunda ]
tags: [camunda, spring boot, bpmn, inclusive gateway]
image: /assets/images/feature-images/feature-image-camunda.png
description: The article contains a step-by-step guide on how to implement a BPMN Inclusive Gateway in Camunda making use of a Spring Boot Application.
comments: true
related_posts:
  - camunda/_posts/2021-01-05-implement-bpmn-parallel-gateway-in-camunda.md
  - camunda/_posts/2021-01-06-implement-bpmn-manual-task-in-camunda.md
---

- Table of Contents
{:toc .large-only}

The article contains a step-by-step guide on how to implement a BPMN Inclusive Gateway in Camunda making use of a Spring Boot Application. Camunda BPM is an open-source workflow and decision automation platform.

## What is an Inclusive Gateway
> “A diverging Inclusive Gateway (Inclusive Decision) can be used to create alternative but also parallel paths within a Process flow. A default path can optionally be identified, to be taken in the event that none of the conditional Expressions evaluate to true. A converging Inclusive Gateway is used to merge a combination of alternative and parallel paths. A control flow token arriving at an Inclusive Gateway MAY be synchronized with some other tokens that arrive later at this Gateway.” [BPMN Inclusive Gateway](/bpmn-inclusive-gateway/)

## Getting Started Guide
The following is a step-by-step guide on how to implement a BPMN Inclusive Gateway in Camunda making use of a Spring Boot Application. 

### Step 1: Create a Spring Boot Application
Create a spring boot application containing the Camunda BPM Engine. Use the Camunda BPM Initializr website to assist you 
in generating a Spring Boot application. Open the following URL in a browser and complete the form to bootstrap your application.

* [https://start.camunda.com/](https://start.camunda.com/)

Fore a more detailed approach on how to create a spring boot application containing the Camunda BPM Engine, use 
the following link:

* [JavaNibble: Camunda Spring Boot Application](/how-to-create-a-camunda-bpm-spring-boot-application/)

### Step 2: Model the Process
Use Camunda Modeller to model the process. The process model is composed of five tasks and two inclusive gateways:

![BPMN Inclusive Gateway](/assets/images/posts/bpmn-inclusive-gateway/bpmn-inclusive-gateway.png){:.lead width="800" height="100" loading="lazy"}
Example of an inclusive gateway
{:.figcaption}

* Place Order: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Order Placed: Is an `Inclusive Gateway` with three sequence flows.
* Coffee Ordered: Is a `Sequence Flow` with an expression `${orderedCoffee==true}`.
* Muffin Ordered: Is a `Sequence Flow` with an expression `${orderedMuffin==true}`.
* Default: Is the default `Sequence Flow`.
* Make Coffee: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Warm up Muffin: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Give Free Sample: Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.
* Deliver Order:Is a `Service Task` linked to a Delegate Expressions with the name `${logger}`.


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
<bpmn:serviceTask id="place-order" name="Place Order" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="make-coffee" name="Make Coffee" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="warm-up-muffin" name="Warm up Muffin" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="give-free-sample" name="Give Free Sample" camunda:delegateExpression="${logger}">
...
<bpmn:serviceTask id="deliver-order" name="Deliver Order" camunda:delegateExpression="${logger}">
```

Configure the service task using the properties panel wihtin the Camunda Modeler.

![Camunda Modeller](/assets/images/posts/bpmn-inclusive-gateway/camunda-modeller-bpmn-inclusive-gateway.png){:.lead width="800" height="100" loading="lazy"}
Camunda Modeller: Service Task Properties
{:.figcaption}

### Step 5: View the Spring Boot Application class
The Spring Boot application is implemented by a class called `BasicInclusiveGatewayApplication`. The class contains the `@SpringBootApplication` annotation that enables the spring boot auto configuration mechanism, enables the component scan on the packages and allow to register extra beans in the context. 

```java
@SpringBootApplication
public class BasicInclusiveGatewayApplication {
  public static void main(String[] args) {
    SpringApplication.run(BasicInclusiveGatewayApplication.class);
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

**Run the command: Scenario 1**

Scenario 1 is starting the Place Order process and passing in the process instance variable called `orderedCoffee` with a value of `true` and the `orderedMuffin` variable with a value of `false`. The inclusive gateway evaluates the variables and directs the token to the applicable service task.

```shell
$ ./start_process_scenario_01.sh
```
The script performs the following commands:

```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/place-order-process/start' --header 'Content-Type: application/json' --data-raw '{
  "variables": {
    "orderedCoffee": {
      "value": "true",
      "type": "boolean"
    },
      "orderedMuffin": {
        "value": "false",
        "type": "boolean"
    }
  }
}'
```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-inclusive-gateway/console-camunda-bpmn-inclusive-gateway-scenario1.png)
Log Statements on Console
{:.figcaption}


**Run the command: Scenario 2**

Scenario 2 is starting the Place Order process and passing in the process instance variable called `orderedCoffee` with a value of `false` and the `orderedMuffin` variable with a value of `true`. The inclusive gateway evaluates the variables and directs the token to the applicable service task.

```shell
$ ./start_process_scenario_02.sh
```
The script performs the following commands:

```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/place-order-process/start' --header 'Content-Type: application/json' --data-raw '{
  "variables": {
    "orderedCoffee": {
      "value": "false",
      "type": "boolean"
    },
      "orderedMuffin": {
        "value": "true",
        "type": "boolean"
    }
  }
}'
```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-inclusive-gateway/console-camunda-bpmn-inclusive-gateway-scenario2.png)
Log Statements on Console
{:.figcaption}

**Run the command: Scenario 3**

Scenario 3 is starting the Place Order process and passing in the process instance variable called `orderedCoffee` with a value of `true` and the `orderedMuffin` variable with a value of `true`. The inclusive gateway evaluates the variables and directs the token to the applicable service task.

```shell
$ ./start_process_scenario_03.sh
```
The script performs the following commands:

```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/place-order-process/start' --header 'Content-Type: application/json' --data-raw '{
  "variables": {
    "orderedCoffee": {
      "value": "true",
      "type": "boolean"
    },
      "orderedMuffin": {
        "value": "true",
        "type": "boolean"
    }
  }
}'
```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-inclusive-gateway/console-camunda-bpmn-inclusive-gateway-scenario3.png)
Log Statements on Console
{:.figcaption}

**Run the command: Scenario 4**

Scenario 4 is starting the Place Order process and passing in the process instance variable called `orderedCoffee` with a value of `false` and the `orderedMuffin` variable with a value of `false`. The inclusive gateway evaluates the variables and directs the token to the applicable service task.
```shell
$ ./start_process_scenario_04.sh
```
The script performs the following commands:
```shell
$ curl --location --request POST 'http://localhost:8080/engine-rest/process-definition/key/place-order-process/start' --header 'Content-Type: application/json' --data-raw '{
  "variables": {
    "orderedCoffee": {
      "value": "false",
      "type": "boolean"
    },
      "orderedMuffin": {
        "value": "false",
        "type": "boolean"
    }
  }
}'
```
The following is the output to the console after running the above command.

![Console](/assets/images/posts/bpmn-inclusive-gateway/console-camunda-bpmn-inclusive-gateway-scenario4.png)
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
The source code used in this example can be found on [Github](https://github.com/javanibble/camunda-bpmn-inclusive-gateway).

## Finally 
Congratulations !!! You have successfully implemented a BPMN Inclusive Gateway in Camunda making use of a Spring Boot Application. 

