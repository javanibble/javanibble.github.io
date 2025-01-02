---
layout: post
title: "List of BPMN Posts"
author: andre
categories: [ software-engineering-topics ]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: 'Master BPMN 2.0: Simplify process modeling with this powerful standard for visualizing, analyzing, and optimizing business workflows effectively.'
comments: true
---

- Table of Contents
{:toc .large-only}

The BPMN 2.0 Topic page contains information about the different types of BPMN diagrams together with the set of
elements used during the modelling process. This also serves as a reference to understand the different bpmn elements,
types and guidelines on each of the elements.

## What is BPMN?
BPMN 2.0 (Business Process Model and Notation 2.0) is a standardised graphical notation for modeling business 
processes. It provides a comprehensive framework for visually representing workflows and interactions across systems 
and participants. 

BPMN 2.0 aims to bridge the gap between business process design and technical implementation, ensuring clear 
communication between business analysts and developers. Its symbols and elements support process documentation, 
analysis, and automation, making it a versatile tool for optimizing organizational operations.

## BPMN  Specifications
Originally developed by the Business Process Management Initiative (BPMI), BPMN has been maintained by the Object Management Group (OMG) since the two organizations merged in 2005. Version 2.0 of BPMN was released in January 2011. Business Process Model and Notation has become the de-facto standard for business processes diagrams.

* **BPMN 2.0.2 Specification**: [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)
* **BPMN 1.2 Specification**: [https://www.omg.org/spec/BPMN/1.2/](https://www.omg.org/spec/BPMN/1.2/)
* **BPMN 1.1 Specification**: [https://www.omg.org/spec/BPMN/1.1/](https://www.omg.org/spec/BPMN/1.1/)
* **BPMN 1.0 Specification**: [https://www.omg.org/spec/BPMN/1.0/](https://www.omg.org/spec/BPMN/1.0/)

## Java Nibble Posts
The following is the set of articles on the Java Nibble blog about BPMN 2.0:

{% assign all_posts = site.tags['bpmn'] | where_exp:"post", "post.url != page.url" %}

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

