---
layout: post
title: "BPMN Escalation Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, escalation event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Escalation Event article provides a detailed explanation of the escalation event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents 
{:toc .large-only}

The BPMN Escalation Event article focus on the definition and usage of the escalation event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the escalation event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the escalation event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Escalation Event?
> "An Escalation identifies a business situation that a Process might need to react to. An Escalation event is used for 
> handling a named Escalation. An escalation has a descriptive name and an escalation code." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the Escalation Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Escalation Event</td><td></td><td><iconify-icon height=48px data-icon="bpmn:start-event-escalation"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-escalation"></iconify-icon></td><td></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-escalation"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-escalation"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-escalation"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:end-event-escalation"></iconify-icon></td></tr>
</table>

BPMN Notation: Escalation Event
{:.figcaption}

## BPMN Event Types
The following table contains a list of the different Escalation Event types, their descriptions and the BPMN notations:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Escalation Event Sub-Process Event (Interrupting) |  | <iconify-icon height=48px data-icon="bpmn:start-event-escalation"></iconify-icon> |
| Escalation Event Sub-process Event (Non-Interrupting) |  | <iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-escalation"></iconify-icon> |
| Escalation Boundary Event (Interrupting) |  | <iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-escalation"></iconify-icon> |
| Escalation Boundary Event (Non-Interrupting) |  | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-escalation"></iconify-icon> |
| Escalation Intermediate Throw Event |  | <iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-escalation"></iconify-icon> |
| Escalation End Event |  | <iconify-icon height=48px data-icon="bpmn:end-event-escalation"></iconify-icon> |

{:.stretch-table}
BPMN Event Types: Escalation Events
{:.figcaption}


## BPMN Diagram
The following is an example of a BPMN Escalation Event within a diagram:

![BPMN Escalation Event](/assets/images/posts/bpmn-escalation-event/bpmn-escalation-event.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Escalation Event
{:.figcaption}


## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Escalation Event as per the official
rules of the BPMN Specification.

* The Escalation End Event MUST have an escalation code. This “throws” the Escalation
* The Escalation Intermediate Throw Event MUST have an escalation code. This “throws” the Escalation.
* The Escalation Boundary Event MAY have an escalation code, since its non-mandatory. This Event “catches” the Escalation. 
* If the Escalation Boundary Event has no escalationCode, then any Escalation SHALL trigger the Event.
* If the Escalation Boundary Event has an escalationCode, then only an Escalation that matches the escalationCode SHALL trigger the Event.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* An Escalation Event that throws the escalation should have a Text Annotation with text “Escalation Code: {Escalation Code}”.

## Finally
This article provided a detailed explanation of the BPMN Escalation Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF






