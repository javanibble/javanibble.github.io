---
layout: post
title: "Articles about Apache Avro"
author: andre
categories: [ software-engineering-topics ]
image: /assets/images/software-engineering/data-platform/learning-apache-avro.png
description: 'A collection of articles and references on Apache Avro.'
comments: true
---

- Table of Contents
{:toc .large-only}

Welcome to the Apache Avro collection on Java Nibble! Here, you'll discover a thoughtfully selected series of posts that 
delve into the core concepts, best practices, and advanced techniques of working with Apache Avro.

Whether you're just starting to explore data serialization or you're an expert optimizing your schema management, this 
page offers valuable insights to help you build efficient, flexible, and scalable data solutions.

## What is Apache Avro?
Apache Avro™ is a robust **_data serialisation framework_** that facilitates the **_exchange of data_** between programs
written in any language.

* Avro is designed for rich data structures and a compact, fast, binary data format.
* Provides a container file for storing persistent data.
* Supports efficient data serialisation and deserialisation.
* Enables remote procedure calls (RPC) for seamless service interaction in distributed environments.
* Offers simple integration with dynamic languages without requiring code generation.

## Official Apache Pages
Here is a list of all the links to official Apache Avro pages, providing access to its documentation, release notes,
and project resources.

* [Apache Avro Documentation](https://avro.apache.org/docs/++version++/)
* [Apache Avro GitHub](https://github.com/apache/avro)

## Collection of Posts
The following is the set of articles on the Java Nibble blog about Apache Kafka:

{% assign all_posts = site.tags['apache-avro'] | where_exp:"post", "post.url != page.url" %}

{% if all_posts.size > 0 %}
<aside class="other-projects related mb0" role="complementary">
  <div class="columns">
    {% for post in all_posts %}
      <div class="column column-1-2">
        {% if post %}
          {% include_cached pro/post-card.html post=post %}
        {% else %}
          Post with path <code>{{ post_path }}</code> not found.
        {% endif %}
      </div>
    {% endfor %}
  </div>
</aside>
{% endif %}

