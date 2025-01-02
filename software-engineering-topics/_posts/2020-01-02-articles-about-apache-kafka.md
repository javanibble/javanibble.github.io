---
layout: post
title: "Articles about Apache Kafka"
author: andre
categories: [ software-engineering-topics ]
image: /assets/images/feature-images/feature-image-kafka.jpg
description: 'A collection of articles and references on Apache Kafka.'
comments: true
---

- Table of Contents
{:toc .large-only}

Welcome to the Apache Kafka collection on Java Nibble! Here, you'll find a carefully curated set of posts covering the 
fundamentals, best practices, and advanced techniques of event streaming with Apache Kafka.

Whether you're a beginner eager to understand messaging systems or an expert fine-tuning your architecture, this page 
provides valuable insights to help you build scalable, reliable, and real-time data pipelines.

## What is Apache Kafka?
Apache Kafka is an open-source distributed event streaming platform designed for building real-time data pipelines and 
streaming applications. It allows you to publish, subscribe to, store, and process large volumes of data with high 
throughput and low latency. 

Kafka is commonly used for stream processing, data integration, and building event-driven architectures. Its 
fault-tolerant design ensures high availability and scalability, making it suitable for handling massive amounts of 
data across distributed systems.

## Collection of Posts
The following is the set of articles on the Java Nibble blog about Apache Kafka:

{% assign all_posts = site.tags['apache-kafka'] | where_exp:"post", "post.url != page.url" %}

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

