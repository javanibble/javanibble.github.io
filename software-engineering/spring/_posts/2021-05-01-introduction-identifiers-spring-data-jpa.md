---
layout: post
title: "An Introduction to Identifiers in Spring Data JPA & Hibernate"
author: andre
categories: [ software-engineering, spring ]
tags: [spring-data]
image: /assets/images/feature-images/feature-image-spring.jpg
description: This article explains the use of Identifiers as primary keys for entities within JPA and Hibernate.
comments: true
---

- Table of Contents
{:toc .large-only}

This article explains the different options in creating identifiers for entities within JPA and Hibernate. 

Identifiers  model the primary key of an entity and are used to uniquely identify a specific entity. The primary key 
uniquely identifies a row within the database. In theory, the identifier does not have to match the primary key, as the 
identifier just need to map to column(s) that uniquely identify each row. The primary key and identifier will used 
interchangeably as part of this article. 

Primary keys/identifiers are bounded by the following constraints:
* `UNIQUE` - The values must uniquely identify each row.
* `NOT NULL` - The values cannot be null. For composite ids, no part can be null.
* `IMMUTABLE` - The values, once inserted, can never be changed.

An identifier might be a single value (simple) or multiple values (composite). Every entity must define an identifier.

## Assigned Identifiers 
JPA specifies that only the following types should be used as identifier attribute types: java primitives, primitive 
wrapper types, `java.lang.String`, `java.util.Date`, `java.sql.Date`, `java.Mmath.BigDecimal` and `java.math.BigInteger`.
Any other types used as an identifier will not be portable.

The following is an example of a simple assigned identifier. The application is responsible for assigning an identifier 
value before invoking the save operation.
```java
@Entity
public class MyEntity {

    @Id
    public Integer id;
}
```

The **@Id Annotation** specifies the primary key of an entity. 
> The mapped column for the primary key of the entity is assumed to be the primary key of the primary table. If no Column annotation is specified, the primary key column name is assumed to be the name of the primary key property or field.

## Generated Identifiers
Hibernate provides the ability for simple identifiers to be generated. This is achieved by adding the `@GeneratedValue` 
annotation to the identifier attribute. Hibernate will generate the identifier value once the entity is persisted.

The `javax.persistence.GeneratedValue` annotation indicates the identifier value is generated. The 
`javax.persistence.GenerationType` indicates how the value will be generated. There are four primary key generation 
strategy types:

* `AUTO` - Indicates that the persistence provider should pick an appropriate strategy for the particular database.
* `IDENTITY` - Indicates that the persistence provider must assign primary keys for the entity using a database identity column.
* `SEQUENCE` - Indicates that the persistence provider must assign primary keys for the entity using a database sequence.
* `TABLE` - Indicates that the persistence provider must assign primary keys for the entity using an underlying database table to ensure uniqueness.

### GenerationType.AUTO
The generation type `GenerationType.IDENTITY` indicates that the persistence provider should pick an appropriate 
strategy for the particular database. The persistence provider decides on how it interprets the AUTO generation type. 
The java type of the identifier attribute provides an indication of how the provider will generate the identifier value.

If the identifier type is numerical (Long, Integer), then Hibernate is going to use the `IdGeneratorStrategyInterpreter` 
to resolve the identifier generator strategy.
```java
@Entity
public class City {

    @Id
    @GeneratedValue
    private Long id;
}
```

If the identifier type is UUID, Hibernate is going to use an UUID identifier. This is supported through its 
`org.hibernate.id.UUIDGenerator` id generator. UUIDGenerator supports pluggable strategies for exactly how the UUID is 
generated. The default strategy is a version 4, but has an alternative strategy which is a RFC 4122 version 1.

```java
@Entity
public class Country {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private UUID id;
}
```

### GenerationType.IDENTITY
The generation type `GenerationType.IDENTITY` indicates that the persistence provider must assign primary keys for the 
entity using a database identity column. The `org.hibernate.id.IdentityGenerator` id generator is used by hibernate and 
expects the identifier to generated by `INSERT` into the table.

```java
@Entity
public class Address {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
}
```

Auto-increment allows a unique number to be generated automatically when a new record is inserted into a table. By 
default, the starting value for `AUTO_INCREMENT` is 1, and it will increment by 1 for each new record.
```sql
CREATE TABLE address (
    id    BIGINT PRIMARY KEY AUTO_INCREMENT,
    ...
);
```

### GenerationType.SEQUENCE
The generation type `GenerationType.SEQUENCE` indicates that the persistence provider must assign primary keys for the 
entity using a database sequence. The `org.hibernate.id.enhanced.SequenceStyleGenerator` id generator is used by hibernate.

```java
@Id
@GeneratedValue(strategy = GenerationType.SEQUENCE)
private Long id;
```

The annotation type `SequenceGenerator` defines a primary key generator that may be referenced by name when a generator 
element is specified for the `GeneratedValue` annotation. The following attributes may be used:
* `name` - A unique generator name that can be referenced by one or more classes to be the generator for primary key values. 
* `sequenceName` - The name of the database sequence object from which to obtain primary key values.
* `initialValue` - The value from which the sequence object is to start generating.
* `allocationSize` - The amount to increment by when allocating sequence numbers from the sequence.

```java
@Entity
public class Store {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator="store-sequence-generator")
    @SequenceGenerator(name = "store-sequence-generator", sequenceName = "user_sequence", initialValue = 5  , allocationSize=1)
    private Long id;
}
```
### GenerationType.TABLE
The generation type `GenerationType.TABLE` Indicates that the persistence provider must assign primary keys for the 
entity using an underlying database table to ensure uniqueness.

The annotation type `TableGenerator` defines a primary key generator that may be referenced by name when a generator 
element is specified for the `GeneratedValue` annotation. The following attributes may be used:
* `name` - A unique generator name that can be referenced by one or more classes to be the generator for id values.
* `table` - Name of table that stores the generated id values.
* `pkColumnName` - Name of the primary key column in the table.
* `valueColumnName` - Name of the column that stores the last value generated.

```java
@Entity
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.TABLE, generator = "table-generator")
    @TableGenerator(name = "table-generator", table = "id_gen", pkColumnName = "gen_name", valueColumnName = "gen_value")
    private Long id;
```

## Generic Generated Identifiers
The `@GenericGenerator` annotation is a hibernate annotation used to denote a custom generator, which can be a class or 
shortcut to a generator supplied by Hibernate. 

### Predefined Hibernate Strategy
There are a number of generic generators supplied by Hibernate that can be used to generate identifiers. All generators 
implement the interface `org.hibernate.id.IdentifierGenerator`. This is a very simple interface. Hibernate provides a 
range of built-in implementations. The fully qualified class name can be used or a shortcut name provided by Hibernate.

**Fully Qualified Class Name**
```java
@Entity
public class MyEntity {

    @Id
    @GeneratedValue(generator = "uuid")
    @GenericGenerator(
        name = "uuid",
        strategy = "org.hibernate.id.UUIDGenerator",
        parameters = {
            @Parameter(
                name = "uuid_gen_strategy_class",
                value = "org.hibernate.id.uuid.CustomVersionOneStrategy"
            )
        }
    )
    public UUID id;
```

**Hibernate Shortcuts**
The shortcut names for the built-in generators are as follows: 
* increment - generates identifiers of type long, short or int that are unique only when no other process is inserting data into the same table.
* identity - supports identity columns in DB2, MySQL, MS SQL Server, Sybase and HypersonicSQL.
* sequence - uses a sequence in DB2, PostgreSQL, Oracle, SAP DB, McKoi or a generator in Interbase.
* hilo - uses a hi/lo algorithm to efficiently generate identifiers of type long, short or int, given a table and column as a source of hi values.
* seqhilo - uses a hi/lo algorithm to efficiently generate identifiers of type long, short or int, given a named database sequence.
* uuid - Generates a 128-bit UUID based on a custom algorithm.
* uuid2 - Generates a IETF RFC 4122 compliant (variant 2) 128-bit UUID.
* guid - uses a database-generated GUID string on MS SQL Server and MySQL.
* native - selects identity, sequence or hilo depending upon the capabilities of the underlying database.
* assigned - lets the application assign an identifier to the object before save() is called.
* select - retrieves a primary key, assigned by a database trigger, by selecting the row by some unique key and retrieving the primary key value.
* foreign - uses the identifier of another associated object.
* sequence-identity - a specialized sequence generation strategy that utilizes a database sequence for the actual value generation

```java
    @Id
    @GeneratedValue(generator = "uuid2")
    @GenericGenerator(name = "uuid2", strategy = "uuid2")
    @Column(columnDefinition = "BINARY(16)")
    private UUID id;
```

### Custom Strategy
To implement a custom strategy fo generating identifiers, the `@GenericGenerator` annotation is used together with the 
fully qualified class name of the custom strategy implementation class. 

```java
@Entity
public class Staff {

    @Id
    @GeneratedValue(generator = "staff_id")
    @GenericGenerator(
        name = "staff_id", 
        strategy = "com.javanibble.springdata.examples.identifier.generator.StaffIdentifierGenerator"
    )
    private Long id;
}
```

The `IdentifierGenerator` interface is the general contract between a class that generates unique identifiers and the 
session. The implementation class of this interface provides a custom identifier generation strategy. The `generate`
method is used to generate a new identifier.

```java
public class StaffIdentifierGenerator implements IdentifierGenerator {
    
    @Override
    public Serializable generate(SharedSessionContractImplementor session, Object obj)  throws HibernateException {
        Random random = new Random();
        int randomId = random.nextInt(1000000);
        return Long.valueOf(randomId);
    }
```

## Composite Identifiers
Composite identifiers correspond to one or more persistent attributes. The composite identifier must be represented by a
primary key class. The primary key class may be defined using the `@EmbeddedId` annotation or defined using the 
`@IdClass` annotation.

### Composite identifiers with @EmbeddedId
The `@EmbeddedId` annotation is applied to a property of an entity class to indicate a composite primary key that is an 
embeddable class. This can also be applied to a mapped superclass. There must be only one `@EmbeddedId` annotation and 
no `@Id` annotation when the `@EmbeddedId` annotation is used.

```java
@Entity
public class Inventory {

    @EmbeddedId
    private InventoryPK id;
```

The embeddable class must be annotated as `@Embeddable`. The `@Embeddable` annotation specifies a class whose instances
are stored as an intrinsic part of an owning entity and share the identity of the entity. Each of the properties of the 
embedded object is mapped to the database table of the entity.

```java
@Embeddable
public class InventoryPK implements Serializable {

    private Long inventory_id;
    private Long secondary_id;

}
```

### Composite identifiers with @IdClass
The `@IdClass` annotation specifies a composite primary key class that is mapped to multiple fields or properties of the
entity.

```java
@Entity
@IdClass(RentalPK.class)
public class Rental {

    @Id
    private Long rental_id;

    @Id
    private Long secondary_id;
```

The names of the properties in the primary key class and the primary key properties of the entity must correspond. The 
types of the  properties myst be the same.

```java
public class RentalPK implements Serializable {

    private Long rental_id;
    private Long secondary_id;

}
```


## Example Code
The source code used in this example can be found on [Github](https://github.com/javanibble/spring-data-examples/tree/master/spring-data-jpa/jpa-identifiers-basic-example).

## Summary
This article explained the different options in creating identifiers for entities within JPA and Hibernate. The article 
explained the relation between the primary key within the database table and the identifier within JPA entity. The 
article also explained how identifiers can be assigned or generated. The article contained multiple examples that 
explained the different strategies to generate identifier values. Finally, the article also explained how to create 
generic generated identifiers and also composite identifiers.

Follow me on any of the different social media platforms and feel free to leave comments.
