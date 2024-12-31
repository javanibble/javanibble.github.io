---
layout: post
title: "BPMN Text Annotation"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, text annotation]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Text Annotation article provides a detailed explanation of the text annotation element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Text Annotation article focus on the definition and usage of the text annotation element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the text annotation. The BPMN Guidelines section
contains a detailed set of rules that apply to the text annotation and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Text Annotation?
> "Text Annotations are a mechanism for a modeller to provide additional text information for the reader of a BPMN 
  Diagram." ~ [BPMN Specification][1]

A Text Annotation is a type of Artifact and is used to provide additional information about the Process. The Text 
Annotation object can be connected to a specific object on the diagram with an Association but does not affect the flow 
of the Process. The text associated with the Text Annotation can be placed within the bounds of the open rectangle.

## BPMN Notation
The BPMN specification defines the Text Annotation element using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Text Annotation | Text Annotations are a mechanism for a moddeler to provide additional text information for the reader of a BPMN Diagram. | <iconify-icon height=48px data-icon="bpmn:text-annotation"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Text Annotation
{:.figcaption}

## BPMN Diagram
The following is an example of a BPMN Text Annotation within a diagram:

![BPMN Text Annotation](/assets/images/posts/bpmn-text-annotation/bpmn-text-annotation.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Text Annotation
{:.figcaption}

## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline 
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Text Annotation as per the official
rules of the BPMN Specification.

* The Text Annotation is an open rectangle that MUST be drawn with a solid single line. 
* The Text Annotations can be used within Choreographies and all BPMN diagrams.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* The Text Annotation should have short and precise information about the "why" the element is doing something. (Not what it is doing)

## Finally
This article provided a detailed explanation of the BPMN Text Annotation element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF