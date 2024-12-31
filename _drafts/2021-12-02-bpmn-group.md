---
layout: post
title: "BPMN Group"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, group]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Group article provides a detailed explanation of the group element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Group article focus on the definition and usage of the group element as documented in the BPMN 2.0 
specification. The example process diagram illustrates the correct use of the group annotation. The BPMN Guidelines 
section contains a detailed set of rules that apply to the group and explains how the element may or may not be used 
within the different BPMN diagrams. 

## What is a Group?
> "The Group object is an Artifact that provides a visual mechanism to group elements of a diagram informally." ~ [BPMN Specification][1]


A Group, like a Text Annotation,  is a type of Artifact and is used to provide additional information about the Process. 
A Group is a grouping of graphical elements that are within the same category of which the name appears on the diagram 
as the group label. Categories can be used for documentation or analysis purposes. A BPMN Group element is one way in 
which categories of objects can be visually displayed and grouped together on a diagram.

A Group, like all Artifacts, is not an activity or any flow object hence it cannot connect to Sequence Flows or Message 
Flows. The BPMN Group element groups together a set of activities, but does not affect the sequence flows between the 
activities within the Group. 

A Group can stretch across the boundaries of a Pool since it is not constrained by restrictions of Pools and Lanes. This
modelling technique is used to identify and group activities that exist within a distributed business-to-business 
transaction.

Groups, unlike a Sub-Process, do not add additional constraints for performance when highlighting certain sub clauses
of a diagram.

## BPMN Notation
The BPMN specification defines the Group element using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Group | A Group is a grouping of graphical elements that are within the same Category. This type of grouping does not affect the Sequence Flows within the Group. The Category name appears on the diagram as the group label. | <iconify-icon height=48px data-icon="bpmn:group"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Group
{:.figcaption}

## BPMN Diagram
The following is an example of a BPMN group within a diagram:

![BPMN Group](/assets/images/posts/bpmn-group/bpmn-group.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Group
{:.figcaption}


## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Group as per the official
rules of the BPMN Specification.

* A Group is a rounded corner rectangle that MUST be drawn with a solid dashed line .
* A Group can be used within Choreographies and all BPMN diagrams.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* A Group SHOULD clearly inform the reader what the group of BPMN element have in common. 
* A Group name SHOULD not be more than five words.


## Finally
This article provided a detailed explanation of the BPMN Group element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF