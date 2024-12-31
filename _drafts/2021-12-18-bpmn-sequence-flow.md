---
layout: post
title: "BPMN Sequence Flow"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, sequence flow]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Sequence Flow article provides a detailed explanation of the sequence flow element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Sequence Flow article focus on the definition and usage of the sequence flow element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the sequence flow annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the sequence flow and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Sequence Flow?
> "A connecting object that shows the order in which activities are performed in a Process and is represented with a 
> solid graphical line. Each Flow has only one source and only one target. A Sequence Flow can cross the boundaries 
> between Lanes of a Pool but cannot cross the boundaries of a Pool." ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Sequence Flow element using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Normal Flow | Normal flow refers to paths of Sequence Flow that do not start from an Intermediate Event attached to the boundary of an Activity. | <iconify-icon height=48px data-icon="bpmn:connection"></iconify-icon> |
| Uncontrolled Flow | Uncontrolled flow refers to flow that is not affected by any conditions or does not pass through a Gateway. The simplest example of this is a single Sequence Flow connecting two Activities.  | <iconify-icon height=48px data-icon="bpmn:connection"></iconify-icon> |
| Conditional Flow | A Sequence Flow can have a condition Expression that are evaluated at runtime to determine whether or not the Sequence Flow will be used.  | <iconify-icon height=48px data-icon="bpmn:conditional-flow"></iconify-icon> |
| Default Flow | For Data-Based Exclusive Gateways or Inclusive Gateways, one type of flow is the default condition flow. This flow will be used only if all the other outgoing conditional flow is not true at runtime.  | <iconify-icon height=48px data-icon="bpmn:default-flow"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Sequence Flow
{:.figcaption}

## Understand Sequence Flows 

### Uncontrolled Flow vs. Controlled Flow

An activity with multiple incoming sequence flows is known as an uncontrolled flow. In the diagram below, the activity
(Step D) will be instantiated when a token arrives from one of the sequence flows. The activity (Step D) will not wait
for the other tokens to arrive. If another token arrives at the activity (Step D) from the same sequence flow or any
other sequence flow, then a separate instance of the activity (Step D) will be created.

![Uncontrolled Flow](/assets/images/posts/bpmn-sequence-flow/uncontrolled_sequence_flow.gif){:.lead width="800" height="100" loading="lazy"}
Uncontrolled Flow
{:.figcaption}

The above diagram will create the following event logs as the token(s) flow through the process: `Process Started`,
`Start Event`, `Step A`, `Step B`, `Step C`, `Step D`, `Step D`, `Step D`, `End Event`, `End Event`, `End Event`, 
`Process Finished`.

If the process requires a controlled flow, then the three sequence flows should converge into a gateway that precedes
the activity (Step D).

![Controlled Flow](/assets/images/posts/bpmn-sequence-flow/controlled_sequence_flow.gif){:.lead width="800" height="100" loading="lazy"}
Controlled Flow
{:.figcaption}

The above diagram will create the following event logs as the token(s) flow through the process: `Process Started`, 
`Start Event`, `Step A`, `Step B`, `Step C`, `Step D`, `End Event`, `Process Finished`.

## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN element.

* Sequence Flows MAY have an Activity as a target. A single activity can have multiple incoming Sequence Flows.
* An Activity without an incoming sequence flow, the activity MUST be instantiated when the process is instantiated. The exception is Compensation and Event Subprocess Activities. 

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

*

## Finally
This article provided a detailed explanation of the BPMN Sequence Flow element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF