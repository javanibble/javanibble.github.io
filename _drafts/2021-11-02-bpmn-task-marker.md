---
layout: post
title: "BPMN Task Marker"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, task marker]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Task Marker article provides a detailed explanation of the task marker, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}


The BPMN Task Marker article focus on the definition and usage of the different types of task markers as documented in 
the BPMN 2.0 specification. The example process diagram illustrates the correct use of the task markers. The BPMN 
Guidelines section contains a detailed set of rules that apply to the task markers and explains how the markers may or 
may not be used within the different BPMN diagrams.

## What is a Task Marker?
> "BPMN specifies three types of markers for a Task: a Loop marker or a Multi-Instance marker and a Compensation marker." ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Task Markers using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Loop |  The marker for a Task that is a standard loop MUST be a small line with an arrowhead that curls back upon itself.  | <iconify-icon height=48px data-icon="bpmn:loop-marker"></iconify-icon> |
| Multi-Instance | The marker for a Task that is a multi-instance MUST be a set of three vertical lines. | <span class="iconify" height=48px data-icon="bpmn:sequential-mi-marker" data-inline="false"></span> <span class="iconify" height=48px data-icon="bpmn:parallel-mi-marker" data-inline="false"></span>
| Compensation | The marker for a Task that is used for compensation MUST be a pair of left facing triangles | <iconify-icon height=48px data-icon="bpmn:compensation-marker"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Task Markers
{:.figcaption}

Task Markers may be used in the following combinations:
* The loop Marker MAY be used in combination with the compensation marker.
* The multi-instance marker MAY be used in combination with the compensation marker.
* The Compensation Marker MAY be used in combination with the loop marker or the multi-instance marker.

## Finally
This article provided a detailed explanation of the BPMN Task Markers. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF