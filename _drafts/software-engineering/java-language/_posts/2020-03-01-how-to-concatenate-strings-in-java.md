---
layout: post
title: "How to Concatenate a String in Java"
author: andre
categories: [ software-engineering, java-language ]
tags: [java]
image: /assets/images/feature-images/feature-image-java.png
description: This post will list a number of examples on how you can concatenate String in Java. 
comments: true
---
- Table of Contents
{:toc .large-only}

There are numerous ways to concatenate Strings making use of the Java language. This post will list a number of examples on how you can concatenate String in Java. 

## Example 1: String Concatenation Operator
The String concatenation operator (`+`) within the Java Language is used to concatenate two operands together as a new String object. 

```java
@Test
@DisplayName("String Concatenation: Operator")
public void testStringConcatWithOperator() {
    String firstName = "Joe";
    String lastName = "Soap";
    String language = "Java";

    String concatMessage = "Hello " + firstName + " " + lastName + ". This is " + language + "!!";
    String expectedValue = "Hello Joe Soap. This is Java!!";

    assertEquals(expectedValue , concatMessage, "The Operator did not create new String as expected.");
}
```

## Example 2: String.concat
The String class provides a `concat` method that concatenates the specified string to the end of this string. If the 
length of the argument string is 0, then this String object is returned. Otherwise, a new String object is created, 
representing a character sequence that is the concatenation of the character sequence represented by this String object 
and the character sequence represented by the argument string.

```java
@Test
@DisplayName("String Concatenation: String.concat")
public void testStringConcatWithStringConcat() {
    String firstName = "Joe";
    String lastName = "Soap";
    String language = "Java";

    String concatMessage = "Hello ".concat(firstName).concat(" ").concat(lastName)
            .concat(". This is ").concat(language).concat("!!");

    String expectedValue = "Hello Joe Soap. This is Java!!";

    assertEquals(expectedValue , concatMessage, "The String Concat did not create new String as expected.");
}
```


## Example 3: StringBuffer (Append method)
A StringBuffer is a thread-safe, mutable sequence of characters and is like a String, but can be modified. The principal 
operations on a StringBuffer are the append and insert methods, which are overloaded so as to accept data of any type. 
Each effectively converts a given datum to a string and then appends or inserts the characters of that string to the 
string buffer. The append method always adds these characters at the end of the buffer; the insert method adds the 
characters at a specified point.

```java
@Test
@DisplayName("String Concatenation: StringBuffer")
public void testStringConcatWithStringBuffer() {
    String firstName = "Joe";
    String lastName = "Soap";
    String language = "Java";

    String concatMessage = new StringBuffer()
            .append("Hello ").append(firstName).append(" ").append(lastName)
            .append(". This is ").append(language).append("!!").toString();

    String expectedValue = "Hello Joe Soap. This is Java!!";

    assertEquals(expectedValue , concatMessage, "The StringBuffer did not create new String as expected.");
}
```

## Example 4: StringBuilder (Append method)
A StringBuilder is a non thread-safe, mutable sequence of characters and is like a String, but can be modified. This 
class provides an API compatible with StringBuffer, but with no guarantee of synchronization. It is recommended that 
this class be used in preference to StringBuffer as it will be faster under most implementations. The principal 
operations on a StringBuilder are the append and insert methods, which are overloaded so as to accept data of any type. 
Each effectively converts a given datum to a string and then appends or inserts the characters of that string to the 
string builder. The append method always adds these characters at the end of the builder; the insert method adds the 
characters at a specified point.

```java
@Test
@DisplayName("String Concatenation: StringBuilder")
public void testStringConcatWithStringBuilder() {
    String firstName = "Joe";
    String lastName = "Soap";
    String language = "Java";

    String concatMessage = new StringBuilder()
            .append("Hello ").append(firstName).append(" ").append(lastName)
            .append(". This is ").append(language).append("!!").toString();

    String expectedValue = "Hello Joe Soap. This is Java!!";

    assertEquals(expectedValue , concatMessage, "The StringBuilder did not create new String as expected.");
}
```

## Example 5: String.format
The String class provides a `format` method that returns a formatted string using the specified format string and 
arguments. The locale always used is the one returned by Locale.getDefault(). The first paramater is a format string, 
and the variable arguments (varargs) are the arguments referenced by the format specifiers in the format string. If 
there are more arguments than format specifiers, the extra arguments are ignored. The number of arguments is variable 
and may be zero.

```java
@Test
@DisplayName("String Concatenation: String.format")
public void testStringConcatWithStringFormat() {
    String firstName = "Joe";
    String lastName = "Soap";
    String language = "Java";

    String concatMessage = String.format("Hello %s %s. This is %s!!", firstName, lastName, language);

    String expectedValue = "Hello Joe Soap. This is Java!!";

    assertEquals(expectedValue , concatMessage, "The String Format did not create new String as expected.");
}
```

## Example 6: String.join
The String class provides a `join` method that returns a new String composed of copies of the CharSequence elements 
joined together with a copy of the specified delimiter. The first paramater is the delimter, and the variable 
arguments (varargs) are the elements to join together. For this example the delimeter is an empty String.

```java
@Test
@DisplayName("String Concatenation: String.join")
public void testStringConcatWithStringJoin() {
    String firstName = "Joe";
    String lastName = "Soap";
    String language = "Java";

    String concatMessage = String.join("", "Hello ", firstName, " ", lastName, ". This is ", language, "!!");

    String expectedValue = "Hello Joe Soap. This is Java!!";

    assertEquals(expectedValue , concatMessage, "The String Join did not create new String as expected.");
}
```

## Example 7: Stream
Stream pipelines may execute either sequentially or in parallel. Collection.stream() creates a sequential stream and the
`collect` method performs a mutable reduction operation on the elements of this stream using a Collector. The 
`Collectors.joining()` method returns a Collector that concatenates the input elements into a String, in encounter order.

```java
    @Test
    @DisplayName("String Concatenation: Streams")
    public void testStringConcatWithStream() {
        String firstName = "Joe";
        String lastName = "Soap";
        String language = "Java";

        String concatMessage = Arrays.asList("Hello ", firstName, " ", lastName, ". This is ", language, "!!")
                .stream().collect(Collectors.joining());

        String expectedValue = "Hello Joe Soap. This is Java!!";

        assertEquals(expectedValue , concatMessage, "The Stream did not create new String as expected.");
    }
```


## Summary
Congratulations! You have successfully learned numerous ways you can concatenate Strings in Java. Follow me on any of the different social media platforms and feel free to leave comments.