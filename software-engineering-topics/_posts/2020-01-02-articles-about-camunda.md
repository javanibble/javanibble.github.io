---
layout: post
title: "Articles about Camunda"
author: andre
categories: [ software-engineering-topics ]
image: /assets/images/feature-images/feature-image-camunda.png
description: 'A collection of articles and references on the Camunda BPM Platform.'
comments: true
---

- Table of Contents
{:toc .large-only}

Welcome to the Camunda collection on Java Nibble! Dive into posts that explore the powerful world of workflow and 
process automation with Camunda. 

From getting started with its BPMN engine to mastering advanced features, this page provides the insights and guidance 
you need to design, execute, and optimize efficient business processes.

## What is Camunda?
Camunda is an open-source platform designed for workflow and business process automation. It leverages BPMN 2.0, 
DMN (Decision Model and Notation), and CMMN (Case Management Model and Notation) standards to model, execute, and 
optimize complex business processes. 

Camunda provides a lightweight, scalable solution that integrates seamlessly with various systems, enabling 
organizations to orchestrate workflows, automate decisions, and achieve operational efficiency. Its developer-friendly 
architecture and robust community support make it a popular choice for both enterprise and agile environments.

### Camunda Important Links
There are many important and interesting information about Camunda. Here are some of the links:
* Camunda BPM Documentation (Latest): [https://docs.camunda.org/manual/latest/](https://docs.camunda.org/manual/latest/)
* Camunda Whitepapers: [https://camunda.com/learn/whitepapers/](https://camunda.com/learn/whitepapers/)
* Camunda Forum: [https://forum.camunda.org/](https://forum.camunda.org/)
* Camunda Webinars: [https://camunda.com/learn/webinars/](https://camunda.com/learn/webinars/)
* Camunda Blog: [https://blog.camunda.com/](https://blog.camunda.com/)
* Camunda Events: [https://camunda.com/events/](https://camunda.com/events/)
* Camunda Source Code: [https://github.com/camunda](https://github.com/camunda)

## Collection of Posts
The following is the set of articles on the Java Nibble blog about Camunda:

{% assign all_posts = site.tags['camunda'] | where_exp:"post", "post.url != page.url" %}

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

