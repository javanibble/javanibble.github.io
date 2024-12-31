---
layout: post
title: "BPMN Message Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, message event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Message Event article provides a detailed explanation of the message event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents 
{:toc .large-only}

The BPMN Message Event article focus on the definition and usage of the message event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the message event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the message event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Message Event?
> "A BPMN Event that references a named message is known as a Message Event. A Message represents the content of a 
> communication between two Participants." ~ [BPMN Specification][1]

Message events are used to send and receive messages between two distinct processes. Message Events may be used as a 
mechanism for two processes to communicate.

## BPMN Notation
The BPMN specification defines the Message Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Message Event</td><td><iconify-icon height=48px data-icon="bpmn:start-event-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-message"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:end-event-message"></iconify-icon></td></tr>
</table>

BPMN Notation: Message Event
{:.figcaption}

## BPMN Event Types
The following table contains a list of the different Message Event types, their descriptions and the BPMN notations:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Message Start Event | A Message arrives from a Participant and triggers the start of the Process. | <iconify-icon height=48px data-icon="bpmn:start-event-message"> |
| Message Event Sub-Process Event (Interrupting) | A Message Event can also initiate an inline Event Sub-Process. A Message Event Sub-Process that interrupts its containing Process is known as a Message Event Sub-Process Event (Interrupting). | <iconify-icon height=48px data-icon="bpmn:start-event-message"> |
| Message Event Sub-process Event (Non-Interrupting) | A Message Event can also initiate an inline Event Sub-Process. A Message Event Sub-Process that does not interrupt its containing Process is known as a Message Event Sub-Process Event (Non-Interrupting). | <iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-message"> |
| Message Intermediate Catch Event | A Message Intermediate Catch Event can be used to receive a Message. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-message"> |
| Message Boundary Event (Interrupting) | A boundary event is an event that is attached to the boundary of an activity. A Message arrives from a participant and triggers the Event. A Message Boundary Event (Interrupting) is attached to an activity and will interrupt the activity. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-message"> |
| Message Boundary Event (Non-Interrupting) | A boundary event is an event that is attached to the boundary of an activity. A Message arrives from a participant and triggers the Event. A Message Boundary Event (Non-Interrupting) is attached to an activity and will not interrupt the activity. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-message"> |
| Message Intermediate Throw Event | A Message Intermediate Throw Event can be used to send a Message. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-message"> |
| Message End Event | A Message End Event can be used to send a Message once the token reach the end event and then terminate the process. | <iconify-icon height=48px data-icon="bpmn:end-event-message"> |

{:.stretch-table}
BPMN Event Types: Message Events
{:.figcaption}


## BPMN Diagram
The following is an example of a BPMN Message Event within a diagram:

![BPMN Message Event](/assets/images/posts/bpmn-message-event/bpmn-message-event.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Message Event
{:.figcaption}


## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Message Event as per the official
rules of the BPMN Specification.

* A Message Intermediate Event MAY be the target for a Message Flow; it can have one incoming Message Flow.
* A Message Intermediate Event MAY be a source for a Message Flow; it can have one outgoing Message Flow.
* A Message Intermediate Event MAY have an incoming Message Flow or an outgoing Message Flow, but not both. 

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* A Message Start Event should have a Text Annotation with text “Receive Message - [Message Name]”.

## Finally
This article provided a detailed explanation of the BPMN Message Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF