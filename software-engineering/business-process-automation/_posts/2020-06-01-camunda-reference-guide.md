---
layout: post
title: "Camunda Reference Guide"
author: andre
categories: [ software-engineering, business-process-automation ]
tags: [camunda]
image: /assets/images/feature-images/feature-image-camunda.png
description: The Reference Guide serve as a starting guide for Camunda with information, examples and links.
comments: true
---

- Table of Contents
{:toc .large-only}

### What is Camunda?
> “Camunda BPM is an open-source workflow and decision automation platform. Camunda BPM ships with tools for creating workflow and decision models, operating deployed models in production, and allowing users to execute workflow tasks assigned to them.” ~ [Wikipedia][1]

---
### Camunda Modeler: BPMN & DMN 
The Camunda Modeller is an application used to model BPMN processes and DMN decisions. The following articles explain how to use the Camunda Modeller to model processes and DMN.  
* [Camunda Modeler Plugins](/plugins-for-camunda-modeler/)
* [How to Model a Simple BPMN Flow using Camunda Modeler](/how-to-model-a-simple-bpmn-flow-using-camunda-modeler/)

---
### Camunda Tutorials with Spring Boot
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can just run. It is possible to run the Camunda BPM Platform within a Spring Boot Application.
* [Guide: Build a Spring Boot Application with Camunda BPM Engine](/guide-build-spring-boot-application-camunda-bpm-engine/)

---
### Official Specifications
Business Process Model and Notation has become the de-facto standard for business processes diagrams.
* BPMN 2.0 Specification: [https://www.omg.org/spec/BPMN](https://www.omg.org/spec/BPMN)
* CMNN 1.1 Specification: [https://www.omg.org/spec/CMMN](https://www.omg.org/spec/CMMN)
* DMN 1.3 Specification: [https://www.omg.org/spec/DMN](https://www.omg.org/spec/DMN)

---
### Camunda Important Links
There are many important and interesting information about Camunda. Here are some of the links: 
* Camunda BPM Documentation (Latest): [https://docs.camunda.org/manual/latest/](https://docs.camunda.org/manual/latest/)
* Camunda Whitepapers: [https://camunda.com/learn/whitepapers/](https://camunda.com/learn/whitepapers/)
* Camunda Forum: [https://forum.camunda.org/](https://forum.camunda.org/)
* Camunda Webinars: [https://camunda.com/learn/webinars/](https://camunda.com/learn/webinars/)
* Camunda Blog: [https://blog.camunda.com/](https://blog.camunda.com/)
* Camunda Events: [https://camunda.com/events/](https://camunda.com/events/)
* Camunda Source Code: [https://github.com/camunda](https://github.com/camunda)

**Posters & Cheat Sheet**
* BPMN 2.0 Poster: [http://www.bpmb.de/images/BPMN2_0_Poster_EN.pdf](http://www.bpmb.de/images/BPMN2_0_Poster_EN.pdf)

---
### Camunda Examples
There are many official Camunda examples that can help you learn the Camunda Platform.

**Camunda Invoice Example**
This is the invoice demo application which is shipped with the full distributions.
* Invoice Example: [https://github.com/camunda](https://github.com/camunda/camunda-bpm-platform/tree/master/examples/invoice)
* BPMN Invoice V1: [invoice.v1.bpmn](https://github.com/camunda/camunda-bpm-platform/blob/master/examples/invoice/src/main/resources/invoice.v1.bpmn) 
* BPMN Invoice V2: [invoice.v1.bpmn](https://github.com/camunda/camunda-bpm-platform/blob/master/examples/invoice/src/main/resources/invoice.v2.bpmn)
* BPMN Review Invoice: [reviewInvoice.bpmn](https://github.com/camunda/camunda-bpm-platform/blob/master/examples/invoice/src/main/resources/reviewInvoice.bpmn)
* DMN Business Decision: [invoiceBusinessDecisions.dmn](https://github.com/camunda/camunda-bpm-platform/blob/master/examples/invoice/src/main/resources/invoiceBusinessDecisions.dmn)

**Camunda Other Examples**
* Camunda BPM Examples: [github.com/camunda/camunda-bpm-examples](https://github.com/camunda/camunda-bpm-examples)

[1]:https://en.wikipedia.org/wiki/Camunda

