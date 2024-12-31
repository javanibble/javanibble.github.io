---
layout: post
title: "Exploring Apache Avro Definitions & Avro Schema"
author: andre
categories: [ software-engineering, data-platform ]
tags: [apache-avro]
image: /assets/images/software-engineering/data-platform/learning-apache-avro.png
description: Apache Avro schema example with primitive types explained.
comments: true
related_posts:
  - software-engineering/data-platform/_posts/2024-04-01-apache-avro-reference-guide.md
  - software-engineering/data-platform/_posts/2024-04-02-an-introduction-to-apache-avro.md
---

- Table of Contents
{:toc .large-only}

Apache Avro is a powerful tool in the big data world that allows for seamless data exchange between different programming languages. Avro is designed to be fast and efficient, making it perfect for real-time data processing and streaming applications such as Apache Kafka.

Avro goes beyond simple data serialisation; it’s a complete framework supporting fast binary data formats, persistent data storage, and efficient service interaction in distributed environments. It’s particularly user-friendly for dynamic languages without the need for code generation.

This guide is designed to demonstrate how Avro can be efficiently used in data projects to simplify the handling of complex data structures and improve performance in big data applications. The example introduces you to the basics of Avro, particularly its primitive types, and explain it using a sample schema for sensor data.


## Apache Avro Definitions
Apache Avro is a serialisation framework designed for efficient data exchange and storage. It supports various schema 
definition formats, including `.avsc`, `.avdl`, and `.avpr`.

Each format serves specific purposes and offers different advantages for defining schemas in Avro. Here’s a detailed 
look at the differences between these formats:

### Avro Schema
* **Format**: `.avsc` files are written in JSON (JavaScript Object Notation) and define the schema for Avro data. This format is directly usable by Avro for serialisation and deserialisation.
* **Use Case**: It’s particularly useful for defining schemas in a language-agnostic way, making it suitable for configurations, data exchange between different programming environments, or when JSON tooling is preferred.

```json
{
  "type": "record",
  "name": "Person",
  "fields": [
    {"name": "name", "type": "string"},
    {"name": "age", "type": "int"}
  ]
}
```

### Avro Interface Definition Language (IDL)
* **Format**: `.avdl` stands for Avro Interface Definition Language. It provides a more human-friendly syntax compared to the JSON schema, resembling the interface definition languages used in RPC systems.
* **Use Case**: IDL is designed for ease of use in writing Avro schemas. It supports defining records, enums, and fixed types in a syntax that is easier for humans to read and write, making it ideal for documentation and initial schema design.
* **Conversion**: `.avdl` files are compiled into `.avsc` JSON format schemas using Avro tools, allowing for the defined schemas to be used in serialisation and deserialisation.

```java
@namespace("com.example")
protocol PersonProtocol {
  record Person {
    string name;
    int age;
  }
}
```

### Avro Protocol
* **Format**: `.avpr` files define Avro protocols in JSON, specifying messages in addition to types. A protocol includes a set of operations, each with its own request and response schema (also potentially error schemas).
* **Use Case**: This format is used for specifying RPC (Remote Procedure Call) interfaces and services, where you need to define not only the data types but also the operations that can be performed on those types.

```json
{
  "protocol": "PersonService",
  "namespace": "com.example",
  "types": [{
    "type": "record",
    "name": "Person",
    "fields": [
      {"name": "name", "type": "string"},
      {"name": "age", "type": "int"}
    ]
  }],
  "messages": {
    "getPerson": {
      "request": [{"name": "name", "type": "string"}],
      "response": "Person"
    }
  }
}
```

### Key Differences
* **Format and Syntax**: `.avsc` uses JSON, `.avdl` uses a custom IDL syntax, and `.avpr` also uses JSON but for defining protocols, including RPC operations.
* **Purpose**: `.avsc` and `.avdl` focus on data structure schemas, while `.avpr` extends to defining service interfaces and operations.
* **Ease of Use**: `.avdl` is generally considered more human-readable and writable compared to the more verbose `.avsc`. `.avpr` is used for more complex RPC service definitions and might not be necessary for simple data serialisation use cases.

Choosing between these formats depends on the specific needs of your project, such as whether you’re defining simple data structures, need human-readable schema definitions, or are designing RPC interfaces and services.

## Avro Schema
Avro Schemas are used to define the structure and data types of data used for serialisation and deserialisation. These schemas can be expressed in JSON in three different ways that cater to various needs and complexities of data representation.

1. **JSON String**: The simplest form, a JSON string, directly names a defined type, such as “string” or “int”. This approach is straightforward and is used for fields that require basic data types. 
2. **JSON Object**: A more detailed form, a JSON object, specifies complex schemas with a defined “type” attribute and additional attributes to further describe the data structure. For example, `{“type”: “record”, … attributes …}` defines a record type with a set of fields. 
3. **JSON Array**: The JSON array form represents a union type, allowing a field to contain data of one of several defined types. This is useful for defining optional fields or fields that can hold multiple types of data, enhancing the schema’s flexibility.

## Avro Schema Using JSON Object
An Avro schema defined using a JSON Object typically follows the layout described below.

This layout allows for the definition of complex types with multiple fields, each field can have its own type, documentation, and default value.

It provides a flexible and powerful way to describe structured data, enabling precise data serialisation and deserialisation according to the schema.

```json
{
  "type": "record", 
  "name": "Example", 
  "namespace": "com.example.avro", 
  "doc": "A description of the record's purpose", 
  "fields": [ 
    {
      "name": "fieldName", 
      "type": "fieldType", 
      "doc": "A description of the field", 
      "default": "defaultValue" 
    },
  ]
}
```

* `type`: Specifies the schema type, “record” for complex types.
* `name`: The name of the record, unique within its namespace.
* `namespace`: (Optional) A string that qualifies the name to avoid name clashes.
* `doc`: (Optional) Documentation for the record, providing insight into its use.
* `fields`: An array containing the definition of each field in the record, including:
* `name`: The name of the field, identifying it within the record.
* `type`: The type of the field, which can be a primitive type (such as “string”, “int”) or another complex type.
* `doc`: (Optional) Documentation for the field, explaining its purpose or usage.
* `default`: (Optional) Default value for the field, used if no value is provided during serialisation.

## Primitive Types in Avro
Apache Avro supports several primitive types that cover the basic data types used in programming. These include:

* `null`: Represents a null value.
* `boolean`: A binary value (true or false).
* `int`: A 32-bit signed integer.
* `long`: A 64-bit signed integer.
* `float`: A single-precision (32-bit) IEEE 754 floating-point number.
* `double`: A double-precision (64-bit) IEEE 754 floating-point number.
* `bytes`: A sequence of 8-bit unsigned bytes.
* `string`: A sequence of Unicode characters.

These primitive types are the building blocks of Avro schemas, allowing developers to precisely define the data structure for efficient serialisation and deserialisation.

## Example Schema: SensorData
To illustrate how Avro schemas are used in practice, consider the following schema for sensor data. The filename of 
the schema is `sensordata.avsc` where the extension of `.avsc` indicates this is an Avro Schema.

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

The `SensorData` schema is a prime example of how Avro can be employed to model intricate data structures in an efficient 
and scalable manner.

Each field is defined with a type that can be a primitive type, such as `string`, `long`, `boolean`, `float`, `double`, 
`bytes`, and `int`, or a complex type.

## Conclusion
Finally, Apache Avro offers a powerful framework for data serialisation, with a flexible schema definition in JSON format that supports both primitive and complex types.

Whether you're working on real-time data processing pipelines with Apache Kafka or building data storage solutions, understanding Avro's capabilities and how to define schemas is crucial for any data engineer or developer.