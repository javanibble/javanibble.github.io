---
layout: post
title: "BPMN Subprocess Marker"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, subprocess marker]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Subprocess Marker article provides a detailed explanation of the subprocess marker, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Subprocess Marker article focus on the definition and usage of the different types of subprocess markers as 
documented in the BPMN 2.0 specification. The example process diagram illustrates the correct use of the subprocess 
markers. The BPMN Guidelines section contains a detailed set of rules that apply to the subprocess markers and explains 
how the markers may or may not be used within the different BPMN diagrams.

## What is a Subprocess Marker?
> "BPMN specifies five types of standard markers for Sub-Processes. The (Collapsed) Sub-Process marker can be combined 
> with four other markers: a loop marker or a multi-instance marker, a Compensation marker, and an Ad-Hoc marker. A 
> collapsed Sub-Process MAY have one to three of these other markers, in all combinations except that loop and 
> multi-instance cannot be shown at the same time." ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Subprocess Markers using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Loop | The marker for a Sub-Process that loops MUST be a small line with an arrowhead that curls back upon itself. | <iconify-icon height=48px data-icon="bpmn:loop-marker"></iconify-icon> |
| Multi-Instance | The marker for a Sub-Process that has multiple instances MUST be a set of three vertical lines in parallel. |  <span class="iconify" height=48px data-icon="bpmn:sequential-mi-marker" data-inline="false"></span> <span class="iconify" height=48px data-icon="bpmn:parallel-mi-marker" data-inline="false"></span>
| Compensation | The marker for a Sub-Process that is used for compensation MUST be a pair of left facing triangles. | <iconify-icon height=48px data-icon="bpmn:compensation-marker"></iconify-icon> |
| Ad-Hoc |  The marker for an ad-hoc Sub-Process MUST be a “tilde” symbol. | <iconify-icon height=48px data-icon="bpmn:ad-hoc-marker"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Subprocess Markers
{:.figcaption}

Sub-process Markers may be used in the following combinations:
* The loop marker MAY be used in combination with any of the other markers except the multi-instance marker.
* The multi-instance marker MAY be used in combination with any of the other markers except the loop marker.
* The compensation marker MAY be used in combination with any of the other markers.
* The ad-hoc marker MAY be used in combination with any of the other markers.

## Finally
This article provided a detailed explanation of the BPMN Subprocess Markers. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF