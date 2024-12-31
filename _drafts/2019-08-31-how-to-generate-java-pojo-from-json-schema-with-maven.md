---
layout: post
title: "How to generate a Java POJO from JSON Schema with Maven"
author: andre
categories: [ Maven ]
tags: [maven, maven-plugin, java, json, json-schema]
image: assets/images/feature-images/feature-image-maven.jpg
description: This article explains the use of the JsonSchema2Pojo maven plugin and how to use it to generate Java types within a Java POJO from a JSON Schema.
comments: true
related_posts:
  - camunda/_posts/2019-09-03-using-the-tenant-rest-interface-of-the-camunda-platform.md
  - camunda/_posts/2019-09-01-using-the-group-rest-interface-of-the-camunda-platform.md
---

- Table of Contents
{:toc .large-only}

This article explains the use of the JsonSchema2Pojo maven plugin and how to use it to generate Java types within a Java POJO from a JSON Schema.

## What is the JsonSchema2Pojo Maven Plugin 


## Getting Started Guide
The following is a step-by-step guide on how to generate Java types within a Java POJO from a JSON Schema making use of the JsonSchema2Pojo maven plugin.

### Step 1: Create a Project with Maven Archetype

```shell
mvn archetype:generate 
	-DgroupId={project-packaging}
	-DartifactId={project-name}
	-DarchetypeArtifactId={maven-template} 
	-DinteractiveMode=false
```
### Step 2: Add the JsonSchema2Pojo 
The POM file is an XML file that contains information about the project and configuration details used by Maven to build the project. For more detail see the [Maven documentation](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

Add the JsonSchema2Pojo maven plugin to the `pom.xml` file.
```xml
    <plugin>
        <groupId>org.jsonschema2pojo</groupId>
        <artifactId>jsonschema2pojo-maven-plugin</artifactId>
        <version>${jsonschema2pojo.version}</version>
        <configuration>
            <sourceDirectory>${basedir}/src/main/resources/schema</sourceDirectory>
            <targetPackage>com.javanibble.maven.example</targetPackage>
        </configuration>
        <executions>
            <execution>
                <goals>
                    <goal>generate</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
```

Add the applicable JsonSchema2Pojo dependencies to the `pom.xml` file.
```xml
    <dependency>
        <groupId>commons-lang</groupId>
        <artifactId>commons-lang</artifactId>
        <version>2.4</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.5.4</version>
    </dependency>
```

### Step 3: Add the JSON Schema
Add the JSON Schema to the `${basedir}/src/main/resources/schema` folder.

### Step 4: Add the JSON Data

### Step 5: Generate the Java POJO

### Step 6: Use Generated POJOs

```java
    ObjectMapper mapper = new ObjectMapper();
    TypeReference<ContactSchema> ref = new TypeReference<ContactSchema>() {};
    InputStream in = JsonSchemaToPojoApplication.class.getClassLoader().getResourceAsStream("json/contact-data.json");
    ContactSchema contactSchema = mapper.readValue(in, ref);
    System.out.println( "Contact Full Name: " + contactSchema.getFirstName() + " " + contactSchema.getLastName() );

    List<EmailAddress> emails = contactSchema.getEmailAddresses();
    for(EmailAddress e : emails) {
        System.out.println("Email:  " + e.getLabel() + " - " + e.getEmail());
    }

    List<PhoneNumber> numbers = contactSchema.getPhoneNumbers();
    for(PhoneNumber n : numbers) {
        System.out.println("Number:  " + n.getLabel() + " - " + n.getNumber());
    }
```

## Compile & Run The Example Permalink
### 1. Compile the application Permalink
Use the following command to compile the Spring Boot application making use of maven:

```shell
$ mvn clean install
```

### 2. Run the application Permalink
After you have successfully built the Camunda BPM Spring Boot application, the compiled artifact can be found in the target directory. Use the following command to start the Camunda BPM Spring Boot Application.

```shell

```

## Example Code Permalink
The source code used in this example can be found on Github.

## Finally Permalink
Congratulations !!! You have successfully 

Refferences
https://mkyong.com/maven/how-to-create-a-java-project-with-maven/
https://baeldung-cn.com/executable-jar-with-maven
https://github.com/joelittlejohn/jsonschema2pojo
https://www.jsonschema2pojo.org/