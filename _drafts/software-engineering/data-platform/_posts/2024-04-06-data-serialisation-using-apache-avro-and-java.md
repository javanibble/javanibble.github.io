---
layout: post
title: "Data Serialisation and Deserialisation using Apache Avro and Java"
author: andre
categories: [ software-engineering, data-platform ]
tags: [apache-avro]
image: /assets/images/software-engineering/data-platform/learning-apache-avro.png
description: A step-by-step guide in defining an Avro schema and using a Java project to serialise and deserialise SensorData objects.
comments: true
related_posts:
  - software-engineering/data-platform/_posts/2024-04-01-apache-avro-reference-guide.md
  - software-engineering/data-platform/_posts/2024-04-02-an-introduction-to-apache-avro.md
---

- Table of Contents
{:toc .large-only}

This guide provides a step-by-step process to master data serialisation and deserialisation using Apache Avro in tandem with Java. By following these straightforward instructions, you’ll effortlessly integrate Avro into your Java applications, streamlining the crucial data interchange processes.

Whether you’re a seasoned Java developer or new to data serialisation, this guide simplifies the complexities of Apache Avro, empowering you to harness its capabilities for seamless serialisation and deserialisation based on a well defined schema.

## Step 1: Defining the Schema
An Avro Schema file can only contain a single schema definition. Avro schemas are defined using JSON and consist of 
primitive types and complex types.

Let’s design an example schema for a “_SensorData_” record. This record will simulate a scenario where various types of 
sensor data are collected, such as in a smart home or industrial setting.

A record definition must include a `type`, a `name`, and `fields`. The fields property are defined as an array of 
objects, each defining a `name` and a `type`. The type attribute of a field is a schema object that can be a primitive 
or complex type.

The schema will include fields for each primitive type to demonstrate their use:

```json
{
  "type": "record",
  "name": "SensorData",
  "namespace": "com.javanibble.avro",
  "doc": "Schema representing various types of data collected from sensors.",
  "fields": [
    {
      "name": "sensorId",
      "type": "string",
      "doc": "A unique identifier for the sensor."
    },
    {
      "name": "timestamp",
      "type": "long",
      "doc": "Timestamp when the data was collected, in milliseconds since the epoch."
    },
    {
      "name": "isActive",
      "type": "boolean",
      "doc": "Indicates if the sensor is active."
    },
    {
      "name": "temperature",
      "type": "float",
      "doc": "Temperature reading from the sensor in Celsius."
    },
    {
      "name": "humidity",
      "type": "double",
      "doc": "Humidity reading from the sensor as a percentage."
    },
    {
      "name": "firmwareVersion",
      "type": "bytes",
      "doc": "Binary data representing the sensor's firmware version."
    },
    {
      "name": "statusMessage",
      "type": "string",
      "doc": "A textual status message about the sensor."
    },
    {
      "name": "errorCount",
      "type": "int",
      "doc": "The number of errors reported by the sensor since last reset."
    }
  ]
}
```

The Avro primitive types are `null`, `boolean`, `int`, `long`, `float`, `double`, `bytes`, and `string`, whereas the 
complex types are `record`, `enum`, `array`, `map`, `union`, and `fixed`.

This “_SensorData_” schema includes:

* `sensorId` (`string`): A textual unique identifier for each sensor.
* `timestamp` (`long`): The time at which the sensor data was collected, represented in milliseconds since the Unix epoch.
* `isActive` (`boolean`): A flag indicating whether the sensor is currently active.
* `temperature` (`float`): A temperature reading from the sensor, represented in Celsius to demonstrate the use of a single-precision floating-point number.
* `humidity` (`double`): A humidity reading from the sensor, shown as a percentage to illustrate the use of a double-precision floating-point number.
* `firmwareVersion` (`bytes`): Binary data representing the version of the sensor's firmware, showing how to handle arbitrary binary data.
* `statusMessage` (`string`): A human-readable message about the sensor's status.
* `errorCount` (`int`): An integer count of any errors the sensor has reported since the last reset.

## Step 2: Maven Configuration
To configure Apache Avro with Maven, you need to include the Avro Maven Dependency and the Avro Maven Plugin in your 
project’s `pom.xml` file.

### Avro Maven Dependency
The Avro Maven Dependency, when included in the project’s `pom.xml`, provides the necessary libraries for seamless 
integration of Apache Avro into Java applications.

Ensure to specify the appropriate version according to your project requirements.

```xml
<dependencies>
      <dependency>
          <groupId>org.apache.avro</groupId>
          <artifactId>avro</artifactId>
          <version>${avro.version}</version>
      </dependency>
</dependencies>
```

### Avro Maven Plugin
The Avro Maven Plugin makes the Avro schema compilation process more efficient. This plugin generates Java classes from 
Avro schema files automatically during the Maven build. It makes it easier to integrate Avro into your project workflow.

```xml
<plugin>
    <groupId>org.apache.avro</groupId>
    <artifactId>avro-maven-plugin</artifactId>
    <version>${avro.version}</version>
    <executions>
        <execution>
            <phase>generate-sources</phase>
            <goals>
                <goal>schema</goal>
            </goals>
            <configuration>
                <sourceDirectory>${project.basedir}/src/main/resources/avro/</sourceDirectory>
                <outputDirectory>${project.build.directory}/generated-sources/avro</outputDirectory>
            </configuration>
        </execution>
    </executions>
</plugin>
```

## Step 3: Compile Schema
To create a Java code example we first need a `SensorData` class definition based on the Avro schema provided earlier.
Since the Avro schema includes various fields, the corresponding Java class should have properties and setter methods 
for each field defined in the schema.

```shell
$ mvn clean install
```

## Step 4: Avro Object Instantiation
Avro generated classes provide three ways for instantiation, each with its own characteristics.

### Example 1: Constructor & Setter Methods
This example illustrates a basic approach to populating an object with setter methods after creating it with a default 
constructor.

```java
SensorData sensorData1 = new SensorData();

sensorData1.setSensorId("sensor_1");
sensorData1.setTimestamp(System.currentTimeMillis());
sensorData1.setIsActive(true);
sensorData1.setTemperature(26.2f);
sensorData1.setHumidity(80.0);
sensorData1.setFirmwareVersion(ByteBuffer.wrap(new byte[]{1, 2, 3, 4}));
sensorData1.setStatusMessage("Operating normally");
sensorData1.setErrorCount(0);
```

### Example 2: Constructor
This example illustrates a basic approach to populating an object as part of the constructor call.

```java
SensorData sensorData2 = new SensorData(
        "sensor_2", 
        System.currentTimeMillis(), 
        true, 
        23.6f, 
        78.0, 
        ByteBuffer.wrap(new byte[]{1, 2, 3, 4}), 
        "Operating normally", 
        0);
```

### Example 3: Builder Pattern
This example illustrates a basic approach to populating an object as part of a builder pattern.

```java
SensorData sensorData3 = SensorData.newBuilder()
        .setSensorId("sensor_3")
        .setTimestamp(System.currentTimeMillis())
        .setIsActive(true)
        .setTemperature(22.2f)
        .setHumidity(65.0)
        .setFirmwareVersion(ByteBuffer.wrap(new byte[]{1, 2, 3, 4}))
        .setStatusMessage("Operating normally")
        .setErrorCount(0)
        .build();
```

In the context of Avro object instantiation, constructors offer better performance since builders create a copy of the data structure before serialisation.

However, builders ensure a more error-resistant process by automatically setting default values and validating data during the setting phase.

## Step 5: Serialisation of Object using Avro Schema
In the provided Java code, we utilise Apache Avro to serialise instances of the `SensorData` class and write them to an 
Avro data file.

```java
DatumWriter<SensorData> sensorDataDatumWriter = new SpecificDatumWriter<SensorData>(SensorData.class);
DataFileWriter<SensorData> dataFileWriter = new DataFileWriter<SensorData>(sensorDataDatumWriter);

dataFileWriter.create(sensorData1.getSchema(), new File("sensordata.avro"));
dataFileWriter.append(sensorData1);
dataFileWriter.append(sensorData2);
dataFileWriter.append(sensorData3);
dataFileWriter.close();
```
* **DatumWriter Creation**: The code initialises a `DatumWriter` for the `SensorData` class. In this case, the `SpecificDatumWriter` is used, which is suitable for generated classes. This class automatically extracts the schema from the specified generated type (`SensorData`).
* **DataFileWriter Creation**: A `DataFileWriter` is created using the previously initialised `DatumWriter`. This writer is responsible for converting Java objects into an in-memory serialised format and writing the serialised records, along with the schema, to a specified Avro data file.
* **File Initialisation**: The `create` method is invoked on the `DataFileWriter` to initialise the Avro data file named `sensordata.avro`.
* **Record Appending**: Instances of the `SensorData` class are sequentially appended to the Avro data file using the `append` method. This step serialises the user objects and writes them, along with their schema, to the Avro data file.
* **File Closure**: To complete the serialisation process, the `close` method is called on the `DataFileWriter`. This ensures that any buffered data is flushed to the file, and the file is properly closed.

## Step 6: Deserialisation of Object using Avro Schema
In the provided Java code, we utilise Apache Avro to deserialise instances of the SensorData class from an Avro data file.

```java
DatumReader<SensorData> sensorDataDatumReader = new SpecificDatumReader<SensorData>(SensorData.class);
DataFileReader<SensorData> dataFileReader = new DataFileReader<SensorData>(new File("sensordata.avro"), sensorDataDatumReader);
SensorData sensorData = null;
while (dataFileReader.hasNext()) {
    sensorData = dataFileReader.next(sensorData);
    System.out.println(sensorData);
}
```

* **DatumReader Creation**: The code initialises a `DatumReader` for the `SensorData` class. Here, the `SpecificDatumReader` is used, which is designed for use with generated classes. This reader automatically extracts the schema from the specified generated type (`SensorData`).
* **DataFileReader Creation**: A `DataFileReader` for the `SensorData` class is created using the previously initialised `DatumReader`. The Avro data file `sensordata.avro` is specified as part of the constructor. This reader is responsible for reading serialised records and their schema from the Avro data file.
* **SensorData Deserialisation**: The code enters a loop that iterates through the Avro data file using the `hasNext` method. Within the loop, each iteration reads the next serialised `SensorData` instance from the file using the next method.
* **Display Data**: The deserialised `SensorData` instance is printed to the console using `System.out.println(sensorData)`. This step demonstrates the successful deserialisation of the Avro data.

## Source Code
The source code for this example can be found on GitHub.

## Conclusion
Finally, the step-by-step guide of Apache Avro has unveiled a robust framework for efficient data serialisation and deserialisation in Java. 

Armed with a deeper understanding of Avro schemas and practical examples, you now possess the tools to optimise data processing and ensure seamless interoperability in their projects.

