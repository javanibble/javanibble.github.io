---
layout: post
title: "BPMN Link Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, link event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Link Event article provides a detailed explanation of the link event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Link Event article focus on the definition and usage of the link event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the link event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the link event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Link Event?
> "The Link Intermediate Events are only valid in normal flow. A Link is a mechanism for connecting two sections of a 
> Process. Link Events can be used to create looping situations or to avoid long Sequence Flow lines. They can also be 
> used as generic “Go To” objects within the Process level." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the Link Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Link Event</td><td></td><td></td><td></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-link"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-link"></iconify-icon></td><td></td></tr>
</table>

BPMN Notation: Link Event
{:.figcaption}

## BPMN Event Types
The following table contains a list of the different Link Event types, their descriptions and the BPMN notations:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Link Intermediate Catch Event | The token traversing a Sequence Flow would arrive at the Link Intermediate Catch Event (Target) after it “jumped” from the Link Intermediate Throw Event (Source) if the Link Name is the same. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-link"></iconify-icon> |
| Link Intermediate Throw Event | The token traversing a Sequence Flow would reach the Link Intermediate Throw Event (Source) and then “jump” to the Link Intermediate Catch Event (Target) if the Link Name is the same. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-link"></iconify-icon> |

{:.stretch-table}
BPMN Event Types: Link Events
{:.figcaption}


## BPMN Diagram
The following is an example of a BPMN Link Event within a diagram:

![BPMN Link Event](/assets/images/posts/bpmn-link-event/bpmn-link-event.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN link Event
{:.figcaption}

The token traversing a Sequence Flow would reach the Link Intermediate Throw Event (Source) and then “jump” to the
Link Intermediate Catch Event (Target) and continue down the Sequence Flow. The Process would continue as if the
Sequence Flow had directly connected the two objects.

## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Link Event as per the official
rules of the BPMN Specification.

* The Link Intermediate Events are only valid in normal flow and MAY NOT be used on the boundary of an Activity. 
* The Link Event are limited to a single Process level and CAN NOT link a parent Process with a Sub-Process.
* The Link Event CAN be multiple source Link Events, but there CAN only be one target Link Event.


### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* A Link Intermediate Throw Event should have a Text Annotation with the `Source: {Link Name}` associated with it.
* A Link Intermediate Catch Event should have a Text Annotation with the `Target: {Link Name}` associated with it.

## Finally
This article provided a detailed explanation of the BPMN Link Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF








