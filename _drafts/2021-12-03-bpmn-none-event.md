---
layout: post
title: "BPMN None Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, none event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN None Event article provides a detailed explanation of the none event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN None Event article focus on the definition and usage of the none event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the none event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the none event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a None Event?
> "A None Event is an event that does not specify an Event Definition and hence the event will not have an internal 
> marker." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the None Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">None Event</td><td><iconify-icon height=48px data-icon="bpmn:start-event-none"></iconify-icon></td><td></td><td></td><td></td><td></td><td></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-none"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:end-event-none"></iconify-icon></td></tr>
</table>
{:.stretch-table}
BPMN Notation: None Event
{:.figcaption}

## BPMN Event Types
The following table contains a list of the different None Event types, their descriptions and the BPMN notations:

| Element | Description | Notation |
|---------|-------------|:--------:|
| None Start Event | The None Start event indicates where a particular process or choreography will start. | <iconify-icon height=48px data-icon="bpmn:start-event-none"></iconify-icon> |
| None Intermediate Event | The None Intermediate Event occurs between the Start Event and the End Event and affects the flow of the Process, but will not start or terminate the Process. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-none"></iconify-icon> |
| None End Event | The None End Event indicates where a process or choreography will end. | <iconify-icon height=48px data-icon="bpmn:end-event-none"></iconify-icon> |

{:.stretch-table}
BPMN Event Types: None Events
{:.figcaption}


## BPMN Diagram
The following is an example of a BPMN None Event within a diagram:

![BPMN None Event](/assets/images/posts/bpmn-none-event/bpmn-none-event.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN None Event
{:.figcaption}


## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN None Event as per the official
rules of the BPMN Specification.

* The None Start Event MAY be used for a top-level Process or any type of Sub-Process (except an Event Sub-Process).
* The None Start Event MAY NOT be used for an Event Sub-Process.
* The None Intermediate Event MUST only be used in normal flow and, thus, MAY NOT be attached to the boundary of an Activity.
* The None End Event MAY be used within any Sub-Process or Process.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* An event should be named using an object and verb to reflect a state.


## Finally
This article provided a detailed explanation of the BPMN None Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF