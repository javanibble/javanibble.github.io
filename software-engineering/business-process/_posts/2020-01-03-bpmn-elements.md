---
layout: post
title: "BPMN 2.0 Elements"
author: andre
categories: [ software-engineering, business-process ]
tags: [bpmn]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "Comprehensive guide to BPMN 2.0 elements and notations."
comments: true
---

- Table of Contents
{:toc .large-only}


Business Process Model and Notation (BPMN) 2.0 is a widely used standard for modelling business processes, visually representing complex workflows.

This article provides a comprehensive reference to BPMN 2.0 elements, explaining the various components that make up process models, including their notations and behaviors.

### BPMN Elements
The basic BPMN modelling elements are very similar to flow diagrams. These elements are grouped into five basic 
categories namely:

* [Flow Objects](#flow-objects) (events, activities, and gateways)
* [Data](#data) (objects, inputs, outputs, stores)
* [Connecting Objects](#connecting-objects) (sequence flows, message flows, and associations)
* [Swimlanes](#swimlanes) (pools and lanes)
* [Artifacts](#artifacts) (groups, and annotations)

## Flow Objects
Flow Objects are the primary elements that define the behavior of a process, consisting of Events, Activities, and 
Gateways. These elements represent actions, decision points, or occurrences within a business process and are connected 
through Sequence Flows to model the process's execution logic. 

| Element               | Description                                                            |                             Notation                              |
|:----------------------|:-----------------------------------------------------------------------|:-----------------------------------------------------------------:|
| [Activity](#activity) | An Activity is a task or process performed within a business workflow. |    <iconify-icon height=48px icon="bpmn:task"></iconify-icon>     |
| [Gateway](#gateway)   | A Gateway controls the flow of a process based on conditions.          |   <iconify-icon height=48px icon="bpmn:gateway"></iconify-icon>   |
| [Event](#event)       | An Event represents something that occurs during a process flow.       | <iconify-icon height=48px icon="bpmn:start-event"></iconify-icon> | 
{:.stretch-table}


### Activity
An Activity represents a task or work that is performed within a business process. It can be either atomic (Task) or 
compound (Sub-Process), with the latter potentially containing its own internal process flow, enabling more complex 
process modeling.

| Element                         | Description                                                                                               |                                  Notation                                  |
|:--------------------------------|:----------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------:|
| [Task](#tasks)                  | A Task is an atomic activity within a Process flow.                                                       |      <iconify-icon height=48px icon="bpmn:task-none"></iconify-icon>       |
| [Sub-Process](#subprocess)      | A Sub-Process is a compound activity that is included within a Process.                                   | <iconify-icon height=48px icon="bpmn:subprocess-collapsed"></iconify-icon> |
| [Call Activity](#call-activity) | A Call Activity is a non-atomic activity that references and invokes an external Process or Global Task.  |    <iconify-icon height=48px icon="bpmn:call-activity"></iconify-icon>     |
{:.stretch-table}


#### Tasks
A Task in is the simplest form of activity, representing a single, atomic unit of work that is performed within a 
business process. It cannot be broken down further and is typically used for actions like sending an email, performing 
a calculation, or making a decision.

| Element            | Description                                                                                  |                                   Notation                                    |
|--------------------|----------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------:|
| Service Task       | A Service Task automates a process step by invoking a system or service.                     |      <iconify-icon height=48px icon="bpmn:service-task"></iconify-icon>       |
| Send Task          | A Send Task is an activity that sends a message to a specified recipient.                    |        <iconify-icon height=48px icon="bpmn:send-task"></iconify-icon>        |
| Receive Task       | A Receive Task is an activity that waits for and processes incoming messages or signals.     |      <iconify-icon height=48px icon="bpmn:receive-task"></iconify-icon>       |
| User Task          | A User Task is an activity performed by a human participant in a process.                    |        <iconify-icon height=48px icon="bpmn:user-task"></iconify-icon>        |
| Manual Task        | A Manual Task is an activity performed without automation, requiring human intervention.     |       <iconify-icon height=48px icon="bpmn:manual-task"></iconify-icon>       |
| Business Rule Task | A Business Rule Task automates decision-making by executing business rules within a process. |   <iconify-icon height=48px icon="bpmn:business-rule-task"></iconify-icon>    |
| Script Task        | A Script Task executes a predefined script or code as part of a process.                     |       <iconify-icon height=48px icon="bpmn:script-task"></iconify-icon>       |
{:.stretch-table}


**Task Markers**

Task Markers are visual indicators placed on tasks to denote specific characteristics or behaviors, such as whether a 
task is a loop, a transaction, or requires user input. These markers enhance the clarity of process models by providing 
additional context and information about how tasks should be executed.

| Task Marker                              | Description                                                                                                                       |                                  Notation                                   |
|:-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------:|
| Loop                                     | This task marker indicates that the task will be repeated until a specific condition is met.                                      |      <iconify-icon height=48px icon="bpmn:loop-marker"></iconify-icon>      |
| Sequential Multi-Instance                | This task marker indicates that multiple instances of a task will be executed one after the other, in a specific order.           | <iconify-icon height=48px icon="bpmn:sequential-mi-marker"></iconify-icon>  | 
| Parallel Multi-Instance                  | This task marker signifies that multiple instances of a task will be executed simultaneously, allowing for concurrent processing. |  <iconify-icon height=48px icon="bpmn:parallel-mi-marker"></iconify-icon>   |
| Compensation                             | This task marker indicates that a task can be reversed with a compensation process.                                               |  <iconify-icon height=48px icon="bpmn:compensation-marker"></iconify-icon>  |
| Ad Hoc                                   | This task marker indicates that a task can be executed in any order or timing.                                                    |     <iconify-icon height=48px icon="bpmn:ad-hoc-marker"></iconify-icon>     |
{:.stretch-table}


#### Subprocess
A Subprocess is an Activity that encapsulates its internal details using Activities, Gateways, Events, and Sequence 
Flows, allowing for a clear representation of complex processes. It can be displayed in a collapsed view, hiding its 
specifics with a distinguishing marker, or in an expanded view, revealing its detailed flow within the containing 
process, and it defines a contextual scope for attribute visibility, transactional handling, and exception management.

| Subprocess Type                    | Description                                                                                                                                                                                                               |                                     Notation                                     |
|:-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------:|
| Subprocess (Expanded)              | An Embedded Subprocess (Expanded) displays its internal flow of activities within the parent process.                                                                                                                     |    <iconify-icon height=48px icon="bpmn:subprocess-expanded"></iconify-icon>     |
| Subprocess (Collapsed)             | An Embedded Subprocess (Collapsed) hides its internal details, represented by a single subprocess marker.                                                                                                                 |    <iconify-icon height=48px icon="bpmn:subprocess-collapsed"></iconify-icon>    |
| Event Subprocess                   | An Event Subprocess is a specialised subprocess that is used within a Process (or Subprocess). An Event Subprocess is not part of the normal flow of its parent Process—there are no incoming or outgoing Sequence Flows. | <iconify-icon height=48px icon="bpmn:event-subprocess-expanded"></iconify-icon>  |
| Transaction Subprocess             | A Transaction Subprocess manages a set of tasks that can be compensated if needed.                                                                                                                                        |        <iconify-icon height=48px icon="bpmn:transaction"></iconify-icon>         |
{:.stretch-table}


**Subprocess Markers**

BPMN specifies five types of standard markers for Subprocesses. The (Collapsed) Subprocess marker can be combined with four other markers: a loop marker or a multi-instance marker, a Compensation marker, and an Ad-Hoc marker. A collapsed Subprocess MAY have one to three of these other markers, in all combinations except that loop and multi-instance cannot be shown at the same time.

| Task Marker               | Description                                                                                                                                                                                |                                  Notation                                   |
|:--------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------:|
| Loop                      | This subprocess marker indicates that a subprocess will repeat until a specific condition is met.                                                                                          |      <iconify-icon height=48px icon="bpmn:loop-marker"></iconify-icon>      |
| Sequential Multi-Instance | This subprocess marker indicates the subprocess will be executed sequentially.                                                                                                             | <iconify-icon height=48px icon="bpmn:sequential-mi-marker"></iconify-icon>  | 
| Parallel Multi-Instance   | This subprocess marker indicates multiple instances are executed simultaneously.                                                                                                           |  <iconify-icon height=48px icon="bpmn:parallel-mi-marker"></iconify-icon>   |
| Ad Hoc                    | This subprocess marker indicates that tasks can be performed in any order.                                                                                                                 |     <iconify-icon height=48px icon="bpmn:ad-hoc-marker"></iconify-icon>     |
| Compensation              | This subprocess marker indicates that the subprocess includes compensation logic, meaning the subprocess can be undone or reversed by triggering specific compensation activities.         |  <iconify-icon height=48px icon="bpmn:compensation-marker"></iconify-icon>  |
{:.stretch-table}

#### Call Activity
A Call Activity is a specialised activity used to invoke a globally defined process or a reusable subprocess from within 
another process. It serves as a placeholder for the referenced process, enabling reuse and modularity, and can call 
either a global task or a process that exists outside the current process model.

| Element                            | Description                                                                            |                               Notation                               |
|:-----------------------------------|:---------------------------------------------------------------------------------------|:--------------------------------------------------------------------:|
| Call Activity                      | A Call Activity invokes a reusable process or subprocess within a larger BPMN process. | <iconify-icon height=48px icon="bpmn:call-activity"></iconify-icon>  |
{:.stretch-table}


### Gateway
Gateways are used to control the flow of a process by determining branching, merging, and joining of paths based on 
specified conditions. They represent decision points that can lead to different process paths, allowing for complex 
logic and flow management within business processes.

| Element              | Description                                                                                          |                                 Notation                                  |
|:---------------------|:-----------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------:|
| Exclusive Gateway    | An Exclusive Gateway routes the process flow to one path based on specific conditions.               |     <iconify-icon height=48px icon="bpmn:gateway-xor"></iconify-icon>     |
| Inclusive Gateway    | An Inclusive Gateway allows one or more paths to be taken based on conditions.                       |     <iconify-icon height=48px icon="bpmn:gateway-or"></iconify-icon>      |
| Parallel Gateway     | A Parallel Gateway is used to synchronize (combine) parallel flows and to create parallel flows.     |  <iconify-icon height=48px icon="bpmn:gateway-parallel"></iconify-icon>   |
| Complex Gateway      | A Complex Gateway handles intricate conditions for routing process flows based on multiple criteria. |   <iconify-icon height=48px icon="bpmn:gateway-complex"></iconify-icon>   |
| Event-based Gateway  | An Event-Based Gateway routes the process flow based on events occurring in the process.             | <iconify-icon height=48px icon="bpmn:gateway-eventbased"></iconify-icon>  |
{:.stretch-table}

### Event
Events signify occurrences that impact the flow of a business process, such as the start, intermediate, or end of a 
process. They can trigger actions or represent results, and are classified into different types, including message 
events, timer events, and error events, providing a comprehensive way to model dynamic process behavior.

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Subprocess <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Subprocess <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">None Event</td><td><iconify-icon height=48px icon="bpmn:start-event-none"></iconify-icon></td><td></td><td></td><td></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-none"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:end-event-none"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Message Event</td><td><iconify-icon height=48px icon="bpmn:start-event-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-message"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:end-event-message"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Timer Event</td><td><iconify-icon height=48px icon="bpmn:start-event-timer"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-timer"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-timer"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-timer"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-timer"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-timer"></iconify-icon></td><td></td><td></td></tr>
<tr><td style="text-align: left;">Escalation Event</td><td></td><td><iconify-icon height=48px icon="bpmn:start-event-escalation"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-escalation"></iconify-icon></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-escalation"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-escalation"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-escalation"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:end-event-escalation"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Conditional Event</td><td><iconify-icon height=48px icon="bpmn:start-event-condition"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-condition"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-condition"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-condition"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-condition"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-condition"></iconify-icon></td><td></td><td></td></tr>
<tr><td style="text-align: left;">Link Event</td><td></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-link"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-link"></iconify-icon></td><td></td></tr>
<tr><td style="text-align: left;">Error Event</td><td></td><td><iconify-icon height=48px icon="bpmn:start-event-error"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-error"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:end-event-error"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Cancel Event</td><td></td><td></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-cancel"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:end-event-cancel"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Compensation Event</td><td></td><td><iconify-icon height=48px icon="bpmn:start-event-compensation"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-compensation"></iconify-icon></td><td></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-compensation"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:end-event-compensation"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Signal Event</td><td><iconify-icon height=48px icon="bpmn:start-event-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-signal"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:end-event-signal"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Multiple Event</td><td><iconify-icon height=48px icon="bpmn:start-event-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-throw-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:end-event-multiple"></iconify-icon></td></tr>
<tr><td style="text-align: left;">Parallel Multiple Event</td><td><iconify-icon height=48px icon="bpmn:start-event-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:start-event-non-interrupting-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px icon="bpmn:intermediate-event-catch-non-interrupting-parallel-multiple"></iconify-icon></td><td></td><td></td></tr>
<tr><td style="text-align: left;">Terminate Event</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td><iconify-icon height=48px icon="bpmn:end-event-terminate"></iconify-icon></td></tr>
</table>


## Data
Data represents information that can be used or produced by activities within a process, serving as inputs or outputs. 
It can take various forms, such as documents, databases, or messages, and is essential for defining the context and 
requirements of process execution. 

| Element      | Description                                                                                       |                              Notation                              |
|:-------------|:--------------------------------------------------------------------------------------------------|:------------------------------------------------------------------:|
| Data Object  | A Data Object represents information used or produced by activities within a BPMN process.        | <iconify-icon height=48px icon="bpmn:data-object"></iconify-icon>  |
| Data Inputs  | Data Inputs are information required by activities to execute tasks within a business process.    |  <iconify-icon height=48px icon="bpmn:data-input"></iconify-icon>  |
| Data Outputs | Data Outputs represent information produced by activities at the conclusion of a process.         | <iconify-icon height=48px icon="bpmn:data-output"></iconify-icon>  |
| Data Stores  | A Data Store represents a persistent repository for storing and retrieving process-related data.  |  <iconify-icon height=48px icon="bpmn:data-store"></iconify-icon>  |
{:.stretch-table}

## Connecting Objects
Connecting Objects are elements that establish relationships between different process components, facilitating the flow
of information and control. They include Sequence Flows, Message Flows, and Associations, each serving a specific 
purpose in linking activities, events, and artifacts within a business process model. 

| Element       | Description                                                                                                       |                             Notation                             |
|:--------------|:------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------:|
| Sequence Flow | Sequence Flow indicates the order of activities and events within a BPMN process.                                 | <iconify-icon height=48px icon="bpmn:connection"></iconify-icon> |
| Message Flow  | Message Flow represents the exchange of messages between different processes or participants in BPMN.             |                                                                  |
| Association   | An Association links artifacts to flow elements, providing additional information without affecting process flow. |                                                                  |
{:.stretch-table}

### Sequence Flow
Sequence Flow indicates the order in which activities and events are executed within a process. It is represented by a 
solid line with an arrowhead, illustrating the progression of the process from one element to another.

| Element           | Description                                                                                                                                                                                             |                                Notation                                |
|:------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------:|
| Normal Flow       | Normal flow refers to paths of Sequence Flow that do not start from an Intermediate Event attached to the boundary of an Activity.                                                                      |    <iconify-icon height=48px icon="bpmn:connection"></iconify-icon>    |
| Uncontrolled Flow | Uncontrolled flow refers to flow that is not affected by any conditions or does not pass through a Gateway. The simplest example of this is a single Sequence Flow connecting two Activities.           |    <iconify-icon height=48px icon="bpmn:connection"></iconify-icon>    |
| Conditional Flow  | A Sequence Flow can have a condition Expression that are evaluated at runtime to determine whether or not the Sequence Flow will be used.                                                               | <iconify-icon height=48px icon="bpmn:conditional-flow"></iconify-icon> |
| Default Flow      | For Data-Based Exclusive Gateways or Inclusive Gateways, one type of flow is the default condition flow. This flow will be used only if all the other outgoing conditional flow is not true at runtime. |   <iconify-icon height=48px icon="bpmn:default-flow"></iconify-icon>   |
{:.stretch-table}

## Swimlanes
Swimlanes are visual elements used to organize and categorize activities and tasks within a process diagram, typically 
representing different participants, roles, or departments involved. They enhance clarity by delineating 
responsibilities and interactions, allowing viewers to easily identify who is responsible for each part of the process. 

| Element  | Description                                                                                  |                               Notation                                |
|:---------|:---------------------------------------------------------------------------------------------|:---------------------------------------------------------------------:|
| Pool     | A Pool represents a participant in a process, encapsulating its activities and interactions. |   <iconify-icon height=48px icon="bpmn:participant"></iconify-icon>   |
| Lane     | A Lane represents a specific participant or role within a Swimlane in a process.             | <iconify-icon height=48px icon="bpmn:lane-divide-two"></iconify-icon> |
{:.stretch-table}

## Artifacts
Artifacts are supplementary elements that provide additional information about the process but do not affect the flow. 
They include Data Objects, Groups, and Annotations, helping to enhance understanding and documentation of the business 
process by providing context and clarification.

| Element          | Description                                                                                                             |                                Notation                                |
|:-----------------|:------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------:|
| Group            | A Group visually organizes related tasks or activities in a process without affecting flow.                             |      <iconify-icon height=48px icon="bpmn:group"></iconify-icon>       |
| Text Annotation  | A Text Annotation provides additional explanatory information about elements within a BPMN diagram.                     | <iconify-icon height=48px icon="bpmn:text-annotation"></iconify-icon>  |
{:.stretch-table}

## Summary
Congratulations! You have finished the post about BPMN 2.0 Elements. Follow me on any of the different social media platforms and feel free to leave comments.

[1]:https://www.omg.org/spec/BPMN/2.0/PDF