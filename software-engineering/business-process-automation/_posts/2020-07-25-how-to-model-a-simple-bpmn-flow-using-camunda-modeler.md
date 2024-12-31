---
layout: post
title: "How to Model a Simple BPMN Flow using Camunda Modeler"
author: andre
categories: [ software-engineering, business-process-automation ]
tags: [camunda]
image: /assets/images/feature-images/feature-image-camunda.png
description: This post contains a step-by-step guide on how to create a simple BPMN flow using Camunda Modeler.
comments: true
---

- Table of Contents
{:toc .large-only}

This post contains a step-by-step guide on how to create a simple BPMN flow using Camunda Modeler. The BPMN flow is called "Personal Message" and contains a single service task that invokes an external service that logs the personal message out to the console. 

## Getting Started
The following list defines the technologies and libraries I used to implement the sample code:

* [Camunda Modeler][Install_Camunda_Modeler]


## Code Example
The code example can be downloaded from Github from the button below. After you have downloaded the code onto your machine, you can open the file in Camunda Modeler.

* [Download Code](https://github.com/andre-mare/camunda-examples/blob/main/basic-bpmn-elements/basic-example/src/main/resources/personal-message.bpmn)

## Step 1: Create a New BPMN Diagram
The first step is to create a new BPMN Diagram. There are several options to perform this task; the simplest is to make use of the new diagram button and select the `Create new BPMN Diagram` menu option. Alternatively, you can make use of the menu options in the following order:

* ___File > New File > BPMN Diagram___

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-01.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-01.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 2: Save the BPMN Diagram
The second step is to save the BPMN Diagram to ensure that you do not accidentally lose your work. Again there are several options, but the simplest is to make use of the save diagram button. You can also make use of the menu options in the following order:

* ___File > Save File___

I saved the BPMN diagram as ***personal-message.bpmn*** on my personal computer.

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-02.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-02.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 3: Set Process Properties
Ensure that you click anywhere on the canvas so that none of the elements are selected. On the left of the modelling canvas, there is a panel that contains all the properties. Once you have selected the `General` tab, you will see the properties of the process called Id, Name, Version Tag, etc..  Set the properties with the following values:

* __Id:__ personal-message
* __Name:__ Personal Message 
* __Version Tag:__ 1.0.0
* __Executable:__ Ticked (Yes)
* __TimeToLive:__ 180

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-03.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-03.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 4: Name the Start Event
The Start Event is modeled as a circle and is already placed by default on the modelling canvas. To name this event, you can double click on the event and type in the name of the event. You can also click on it once, and set the name in the properties panel under the `General` tab.

* ___Name:___ Retrieve Personal Message

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-04.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-04.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 5: Create and name the Task
The next step is to append a task to the Start Event. Once you have clicked on the event once, you will see multiple options to the right of the event. You can select the `Append Task` option which will create a task as the next step of your flow. To name this task, you can double click on the task and type in the name of the task. You can also click on it once, and set the name in the properties panel under the `General` tab.

* ___Name:___ Log on Console

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-05.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-05.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 6: Change Task Type to Service Task
Task types specify the nature of the action that will be performed as part of the process. In this example, we will change the task to a `Service Task`. Click on the task once to see the multiple options (icons) to the right of the task. The wrench icon allows you to change the type of the task. Select the `Service Task` option from the menu after you have clicked on the wrench icon.

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-06.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-06.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 7: Set the Task Properties (General)
Ensure that you click on the service task to display the properties of the task in the properties panel. Once you have selected the `General` tab, you will see the properties of the task called Id, Name, etc..  Set the properties with the following values:

* __Id:__ service-task-log-on-console
* __Name:__ Log on Console 

The implementation details evaluates an expression that resolves to a delegation object. This will be used in other examples to invoke a Java Delegate with the name `logger`.

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-07.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-07.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>


## Step 8: Set the Task Implementation
After you have set the general properties of the service task, you must also configure the implementation details. Ensure that you are on the `General` tab of the properties panel. In the details section of the tab, you will find the implementation details. Add the following values into the properties:

* __Implementation Details:__ Delegate Expression 
* __Delegate Expression:__ ${logger}  

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-08.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-08.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>

## Step 9: Create End Event
The final step is to create an End Event for our process. Click on the service task once to see the multiple options (icons) to the right of the task. Select the dark bold circle the append an `End Event` after the task. To name this event, you can double click on the event and type in the name of the event. You can also click on it once, and set the name in the properties panel under the `General` tab.

* ___Name:___ Personal Message Retrieved

<a href="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-09.png"><img src="{{site.baseurl}}/assets/images/posts/simple-bpmn-flow-camunda-modeler/personal-message-09.png" width="100%"/></a>
<p style="text-align:center">Click To Enlarge</p>

## Remember: Save the Process
As you have already saved the process to a specific file, you can only click on the `Save` icon in the toolbar. Alternatively, you can make use of the menu options in the following order:

* ___File > Save File___

## Summary
Congratulations! You have successfully modelled a simple process in the Camunda Modeler. This process contains a single `Service Task` that will log a personal message to the console. Follow me on any of the different social media platforms and feel free to leave comments.

[Install_Camunda_Modeler]:https://camunda.com/download/modeler/