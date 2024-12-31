---
layout: post
title: "BPMN Call Activity"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, call activity]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Call Activity article provides a detailed explanation of the call activity element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Call Activity article focus on the definition and usage of the call activity element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the call activity. The BPMN Guidelines section
contains a detailed set of rules that apply to the call activity and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Call Activity?
> "A Call Activity identifies a point in the Process where a global process or a global task is used." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the Call Activity using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Call Activity | A Call Activity identifies a point in the Process where a global Process or a Global Task is used. The Call Activity acts as a ‘wrapper’ for the invocation of a global Process or Global Task within the execution. The activation of a call Activity results in the transfer of control to the called global Process or Global Task. | <iconify-icon height=48px data-icon="bpmn:call-activity"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Call Activity
{:.figcaption}


## Finally
This article provided a detailed explanation of the BPMN Call Activity element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF