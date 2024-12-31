---
layout: post
title: "How to Create a Console Application using CommandLineRunner (Part 2)"
author: andre
categories: [ spring-boot ]
tags: [spring-boot, spring, java]
image: /assets/images/feature-images/feature-image-spring.jpg
description: This article describes how to create a Spring Boot application and make use of multiple CommandLineRunner classes.
comments: true
---


This article describes how to create a Spring Boot application and make use of multiple CommandLineRunner beans within 
the same application context. The order in which different beans execute the run methods, is controlled by the @Order 
annotation. 


## Multi-part Series
This article is part of a multi-part series on how to create a console application using the CommandLineRunner.

* [How to Create a Console Application using CommandLineRunner (Part 1)][Article1]
* [How to Create a Console Application using CommandLineRunner (Part 2)][Article2]


## Getting Started Guide
The following is a step-by-step guide on how to create a Console Application making use of the `CommandLineRunner` interface within Spring Boot.


### Step 1: Create a Spring Boot Application
The very first step is to create a Spring boot Application. Use the Spring Initializr website to assist you 
in generating a Spring Boot application. Open the following URL in a browser and complete the form to bootstrap your application.

* [https://start.spring.io/](https://start.spring.io/)


### Step 2: Define Maven Dependencies
The following dependencies should be included in the pom.xml file:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>   
```


## Step 3: Create a Spring Boot Application
The console application is implemented by a class called *MultiConsoleApplication*. The class contains the *@SpringBootApplication* annotation that enables the spring boot auto configuration mechanism, enables the component scan on the packages and allow to register extra beans in the context. 

```java
@SpringBootApplication
public class MultiConsoleApplication {

    private static Logger LOG = LoggerFactory.getLogger(MultiConsoleApplication.class);

    public static void main(String[] args) {
        SpringApplication.run(MultiConsoleApplication.class, args);    
    }

}
```


## Step 3: Implement two CommandLineRunner beans
The *CommandLineRunner1* class implements the *CommandLineRunner* interface. This Interface is used to indicate that a 
bean should run when it is contained within a SpringApplication. The run method will be invoked after the application 
context has been loaded. 

The *@Order* annotation is used to indicate the order in which the multiple CommandLineRunner' *run()* methods will be 
executed. *@Order(2)* indicates it will run second after the other CommandLineRunner bean finish.

```java
@Component
@Order(2)
public class CommandLineRunner1 implements CommandLineRunner {

    private static Logger LOG = LoggerFactory.getLogger(CommandLineRunner1.class);

    @Override
    public void run(String... args) {
        LOG.info("CommandLineRunner 1: Now Executing ");
    }
}
```

The *CommandLineRunner2* class also implements the *CommandLineRunner* interface.  

*@Order(1)* indicates it will run first.

```java
@Component
@Order(1)
public class CommandLineRunner2 implements CommandLineRunner {

    private static Logger LOG = LoggerFactory.getLogger(CommandLineRunner2.class);

    @Override
    public void run(String... args) {
        LOG.info("CommandLineRunner 2: Now Executing ");
    }
}
```

## Compile and Run the Application
Use the following command to compile the Spring Boot application making use of maven.

**Build Application**
```shell
$ mvn clean install
```

After you have successfully built the Spring Boot application, the compiled artifact can be found in the target 
directory. There are two ways to run the Spring Boot Application.

**Run Application**
```shell
# Option 1: Use the maven Spring Boot plugin to run the application.
$ mvn spring-boot:run 

# Option 2: Use the java command to run the application
$ java -jar target/multi-console-application-0.0.1-SNAPSHOT.jar
```
 
## Example Code
The source code used in this example can be found on [Github](https://github.com/javanibble/spring-boot-examples/tree/master/console-application/multi-console-application).

## Finally 
Congratulations !!! You have successfully implemented a Spring Boot application using the CommandLineRunner to read values from the command line and print them out. You control the order in which different beans execute their run methods by using the @Order annotation.

[Article1]:/how-to-create-a-console-application-using-commandlinerunner-part-1
[Article2]:/how-to-create-a-console-application-using-commandlinerunner-part-2