---
layout: post
title: "How to Create a Console Application using CommandLineRunner (Part 1)"
author: andre
categories: [ spring-boot ]
tags: [spring-boot, spring, java]
image: /assets/images/feature-images/feature-image-spring.jpg
description: This article describes how to create a Spring Boot application and make use of the CommandLineRunner to read values from the command line and print them out.
comments: true
---

- Table of Contents
{:toc .large-only}

This article describes how to create a Spring Boot application and make use of the CommandLineRunner to read values from the command line and print them out.


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

### Step 3: Implement the CommandLineRunner Interface
The console application is implemented by a class called `SimpleConsoleApplication`. The class contains the 
`@SpringBootApplication` annotation that enables the spring boot autoconfiguration mechanism, enables the component 
scan on the packages and allow to register extra beans in the context. 

The `SimpleConsoleApplication` class also implements the `CommandLineRunner` interface. This interface is used to 
indicate that a bean should run when it is contained within a SpringApplication. The run method will be invoked after 
the application context has been loaded.

The `run` method prints the arguments it received as arguments what the application was started. 

```java
@SpringBootApplication
public class SimpleConsoleApplication implements CommandLineRunner { 
    private static Logger LOG = LoggerFactory.getLogger(SimpleConsoleApplication.class);
    
    public static void main(String[] args) {
        SpringApplication.run(SimpleConsoleApplication.class, args);
    }

    @Override
    public void run(String... args) {
        LOG.info("Printing Command Line Arguments: ");

        for (int i = 0; i < args.length; ++i) {
            LOG.info("args[{}]: {}", i, args[i]);
        }
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
$ mvn spring-boot:run -Dspring-boot.run.arguments="Hello World"

# Option 2: Use the java command to run the application
$ java -jar target/simple-console-application-0.0.1-SNAPSHOT.jar Hello World
```

## Example Code
The source code used in this example can be found on [Github](https://github.com/javanibble/spring-boot-examples/tree/master/console-application/simple-console-application).

## Finally 
Congratulations !!! You have successfully implemented a Spring Boot application using the CommandLineRunner to read values from the command line and print them out. 

[Article1]:/how-to-create-a-console-application-using-commandlinerunner-part-1
[Article2]:/how-to-create-a-console-application-using-commandlinerunner-part-2