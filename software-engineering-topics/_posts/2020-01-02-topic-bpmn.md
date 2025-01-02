---
layout: post
title: "Topic: BPMN 2.0"
author: andre
categories: [ software-engineering-topics ]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: 'Master BPMN 2.0: Simplify process modeling with this powerful standard for visualizing, analyzing, and optimizing business workflows effectively.'
comments: true
related_posts:
  - software-engineering/business-process-automation/_posts/2020-01-02-bpmn-diagrams.md
  - software-engineering/business-process-automation/_posts/2020-01-03-bpmn-elements.md
all_posts:  
  - software-engineering/business-process-automation/_posts/2020-01-02-bpmn-diagrams.md
  - software-engineering/business-process-automation/_posts/2020-01-03-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN 2.0 Topic page contains information about the different types of BPMN diagrams together with the set of
elements used during the modelling process. This also serves as a reference to understand the different bpmn elements,
types and guidelines on each of the elements.

## What is BPMN?
> "Business Process Model and Notation has become the de-facto standard for business processes diagrams. It is intended
> to be used directly by the stakeholders who design, manage and realize business processes, but at the same time be
> precise enough to allow BPMN diagrams to be translated into software process components. BPMN has an easy-to-use
> flowchart-like notation that is independent of any particular implementation environment." ~ [BPMN Specification](https://www.omg.org/spec/BPMN/2.0.2/)

## BPMN  Specifications
Originally developed by the Business Process Management Initiative (BPMI), BPMN has been maintained by the Object Management Group (OMG) since the two organizations merged in 2005. Version 2.0 of BPMN was released in January 2011. Business Process Model and Notation has become the de-facto standard for business processes diagrams.

* **BPMN 2.0.2 Specification**: [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)
* **BPMN 1.2 Specification**: [https://www.omg.org/spec/BPMN/1.2/](https://www.omg.org/spec/BPMN/1.2/)
* **BPMN 1.1 Specification**: [https://www.omg.org/spec/BPMN/1.1/](https://www.omg.org/spec/BPMN/1.1/)
* **BPMN 1.0 Specification**: [https://www.omg.org/spec/BPMN/1.0/](https://www.omg.org/spec/BPMN/1.0/)

## Java Nibble Posts
The following is the set of articles on the Java Nibble blog about BPMN 2.0:

{% assign post = page %}

{% if page.related_posts %}
{% if major >= 4 and minor >= 1 %}
{% assign related_posts = site.posts | where_exp:"post", "page.related_posts contains post.path or page.related_posts contains post.url" %}
{% else %}
{% assign related_posts_1 = site.posts | where_exp:"post", "page.related_posts contains post.path" %}
{% assign related_posts_2 = site.posts | where_exp:"post", "page.related_posts contains post.url" %}
{% assign related_posts = related_posts_1 | concat:related_posts_2 %}
{% endif %}
{% elsif site.hydejack.use_lsi or site.use_lsi %}
{% assign related_posts = site.related_posts %}
{% elsif post.categories.first %}
{% assign related_posts = site.categories[post.categories.first] | where_exp:"post", "post.url != page.url" %}
{% elsif post.tags.first %}
{% assign related_posts = site.tags[post.tags.first] | where_exp:"post", "post.url != page.url" %}
{% else %}
{% assign related_posts = site.related_posts %}
{% endif %}

{% if related_posts.size > 0 %}
<aside class="related mb4" role="complementary">
  <h2 class="hr-bottom">{{ site.data.strings.related_posts | default:"Related Posts" }}</h2>

  <ul class="related-posts">
    {% for post in related_posts limit:3 %}
      {% if post %}
        {% include_cached components/post-list-item.html post=post %}
      {% else %}
        <li>Post with path <code>{{ post_path }}</code> not found.</li>
      {% endif %}
    {% endfor %}
  </ul>
</aside>
{% endif %}

