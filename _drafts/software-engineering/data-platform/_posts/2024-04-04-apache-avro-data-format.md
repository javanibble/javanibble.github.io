---
layout: post
title: "Apache Avro Data Format"
author: andre
categories: [ software-engineering, data-platform ]
tags: [apache-avro]
image: /assets/images/software-engineering/data-platform/learning-apache-avro.png
description: Explore the Inner Workings of the Apache Avro Data Format and Tools
comments: true
related_posts:
  - software-engineering/data-platform/_posts/2024-04-01-apache-avro-reference-guide.md
  - software-engineering/data-platform/_posts/2024-04-02-an-introduction-to-apache-avro.md
---

- Table of Contents
{:toc .large-only}

Apache Avro is a widely used data serialisation system known for its compact, efficient, and flexible format. It facilitates data exchange between systems with different architectures and languages, making it a popular choice for big data applications and distributed computing environments.

In this blog, we will explore the practical applications of Avro, delve into its key components, and provide hands-on examples for writing to and reading from Avro files using Java.

Additionally, we will cover the utility of the Apache Avro Tools JAR for inspecting and manipulating Avro data files. 


## Practical Applications of Apache Avro
Apache Avro is versatile and finds use in various scenarios across data storage, data interchange, and stream processing 
due to its efficient and compact serialization format.

- **Data Storage**: Avro files are commonly used for storing large volumes of data, such as in data lakes or big data platforms.
- **Data Interchange**: Avro is used for data interchange between different systems, particularly in distributed computing environments.
- **Stream Processing**: Avro is often used in stream processing systems, such as Apache Kafka, for serializing messages.

## Key Components of Apache Avro Data Format
The `.avro file` extension is used for files that are formatted according to the Apache Avro data serialisation system. 
Apache Avro is a framework for data serialisation, which provides a compact, fast, binary data format, along with a rich 
data structure definition language.

### Schema Definition
- **Schema Definition**: The schema is defined using JSON and describes the structure of the data. It includes information about data types and the hierarchical structure of the records.
- **Self-describing File**: The schema is stored alongside the data within the Avro file, making the file self-describing. This allows any program that understands Avro to read the data without needing external schema definitions.

### Data Serialisation
- **Binary Format**: Avro serialises data into a compact binary format, which is efficient for both storage and transmission. This binary format reduces the overhead and size of the data compared to text-based formats like JSON.
- **Blocks**: Data is stored in blocks within the Avro file. Each block contains a series of records and can be compressed to save space. This block structure also facilitates splitting the file for distributed processing, such as in Hadoop’s MapReduce.

### File Header
- **Metadata**: The header of an Avro file includes metadata about the file, such as the schema and synchronization markers. These markers help in identifying the boundaries of blocks, which is useful for parallel processing.
- **Sync Marker**: The sync marker is a unique identifier that helps in splitting the file and ensuring data integrity during distributed processing.

### Compression
- **Supported Codecs**: Avro supports various compression codecs like `snappy` and `deflate`. Compression can be configured when writing data to Avro files, optimizing storage and performance.

## Practical Examples
This section provides an example schema and demonstrates how to use Java code for writing data to an Avro file and reading data from an Avro file.

### Example Avro Schema
The following schema defines a `SensorData` record with various fields such as sensor ID, timestamp, activity status, temperature, humidity, firmware version, status message, and error count, illustrating the structure of data that can be serialized using Apache Avro.

```json
{
  "type": "record",
  "name": "SensorData",
  "namespace": "com.example",
  "fields": [
    {"name": "sensorId", "type": "string"},
    {"name": "timestamp", "type": "long"},
    {"name": "isActive", "type": "boolean"},
    {"name": "temperature", "type": "float"},
    {"name": "humidity", "type": "double"},
    {"name": "firmwareVersion", "type": "bytes"},
    {"name": "statusMessage", "type": "string"},
    {"name": "errorCount", "type": "int"}
  ]
}
```

### Example Java Code for Writing to an Avro File
The following Java code demonstrates how to write data to an Avro file using a predefined schema, including creating a 
`GenericRecord`, populating it with data, and saving it to a specified file path.

```java
public class AvroWriteExample {
    public static void main(String[] args) throws IOException {
        // Load the schema
        Schema schema = new Schema.Parser().parse(new File("path/to/sensordata.avsc"));

        // Create a record
        GenericRecord record = new GenericData.Record(schema);
        record.put("sensorId", "sensor_1");
        record.put("timestamp", System.currentTimeMillis());
        record.put("isActive", true);
        record.put("temperature", 22.5f);
        record.put("humidity", 55.0);
        record.put("firmwareVersion", ByteBuffer.wrap(new byte[]{1, 2, 3, 4}));
        record.put("statusMessage", "All systems operational");
        record.put("errorCount", 0);

        // Write the record to an Avro file
        File avroFile = new File("path/to/sensordata.avro");
        DatumWriter<GenericRecord> datumWriter = new GenericDatumWriter<>(schema);
        DataFileWriter<GenericRecord> dataFileWriter = new DataFileWriter<>(datumWriter);
        dataFileWriter.create(schema, avroFile);
        dataFileWriter.append(record);
        dataFileWriter.close();
    }
}
```

### Example Java Code for Reading from an Avro File
The following Java code illustrates how to read data from an Avro file using a predefined schema, including loading the 
schema, reading the Avro file, and printing the contents of the records.

```java
public class AvroReadExample {
    public static void main(String[] args) throws IOException {
        // Load the schema
        Schema schema = new Schema.Parser().parse(new File("path/to/sensordata.avsc"));

        // Read the record from an Avro file
        File avroFile = new File("path/to/sensordata.avro");
        DatumReader<GenericRecord> datumReader = new GenericDatumReader<>(schema);
        DataFileReader<GenericRecord> dataFileReader = new DataFileReader<>(avroFile, datumReader);

        GenericRecord record = null;
        while (dataFileReader.hasNext()) {
            record = dataFileReader.next(record);
            System.out.println(record);
        }
        dataFileReader.close();
    }
}
```

## Apache Avro Tools JAR
The Apache Avro Tools JAR is a versatile utility that provides a suite of command-line tools for working with Avro files.

These tools enable operations such as viewing contents, converting data to and from JSON, and extracting schemas, thus allowing users to inspect and manipulate Avro data quickly without the need for custom code.

### Download Avro Tools JAR
To ensure you are always using the latest version of Avro Tools, you can check the Maven Central Repository for the 
latest versions and corresponding download links.

```shell
# Download the Avro Tools JAR from the Maven Repository
$ wget https://repo1.maven.org/maven2/org/apache/avro/avro-tools/1.11.3/avro-tools-1.11.3.jar
```

### Using Avro Tools JAR
Once downloaded, you can use the Avro Tools JAR for various operations. Here are a few examples:

**Convert Avro to JSON:**

To view the contents of an Avro file in a human-readable format, you can use the Avro Tools JAR to convert Avro data to JSON by running the following command:

```shell
$ java -jar avro-tools-1.11.3.jar tojson --pretty input.avro
```

**Get Schema from Avro File:**

To extract and view the schema from an Avro file, you can use the Avro Tools JAR by executing the following command:

```shell
$ java -jar avro-tools-1.11.3.jar getschema input.avro
```

**Convert JSON to Avro:**

To convert a JSON file to an Avro file using a specified schema, you can use the Avro Tools JAR with the following command:

```shell
$ java -jar avro-tools-1.11.3.jar fromjson --schema-file schema.avsc input.json > output.avro
```

## Conclusion
Apache Avro’s efficient serialization format and robust schema management make it an invaluable tool for handling large volumes of data across various platforms.

Developers can effectively utilise Avro for data storage, interchange, and stream processing by understanding its essential components and practical applications.

Whether managing data lakes or implementing real-time data pipelines, Apache Avro offers a reliable and performant solution.