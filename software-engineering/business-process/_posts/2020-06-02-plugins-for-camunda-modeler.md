---
layout: post
title: "Plugins for Camunda Modeler"
author: andre
categories: [ software-engineering, business-process ]
tags: [camunda]
image: /assets/images/feature-images/feature-image-camunda.png
description: The article contains a list of free plugins that can be included in the Camunda Modeler.
comments: true
---

- Table of Contents
{:toc .large-only}

This article lists the most popular Camunda Modeler plugins like Autosave, BPMN Token Simulation, Transaction Boundaries Visualization, Technical Tooltips, and many more. The plugins allow you to change the behaviour and appearance of Camunda Modeler. The article furthermore contains an explanation of how to install the plugins. 

## What is Camunda Modeler
Camunda Modeler is a user-friendly desktop application and is used to create and edit BPMN process diagrams and DMN decision tables. It is available on Windows, Linux and Mac operating systems. It is possible to view and edit BPMN 2.0 diagrams in parallel within multiple tabs.
Camunda Modeler allows for the edit of execution-related BPMN 2.0 properties within the built-in properties panel.

It is possible to extend the functionality of Camunda Modeler via plugins. There are several open-source plugins
available developed by the ever-growing Camunda Community.

## How to install plugins
At present, the Camunda Modeler does not have a very seamless way to install plugins. Up until recently, the plugins were 
published by developers within their personal GitHub repositories. There are also several plugins available in the 
[Camunda Community Hub](https://github.com/camunda-community-hub). 

The Camunda Modeler Plugins can be installed by cloning the Git repositories within the Camunda Modeler Plugins directory `{MODELER_LOCATION}/plugins`. You 
can also copy the directory to the plugin directory if you have cloned it to a different location. The plugin directory can be found here:
* Windows: `C:\Users\{user_name}\AppData\Roaming\camunda-modeler\resources\plugins`
* MacOS: `/Users/{user_name}/Library/Application Support/camunda-modeler/plugins`

On MacOS you have to create the `plugin` directory yourself.

## Popular Camunda Modeler Plugins 
The following list contains all the popular Camunda Modeler Plugins currently available:

### 1. AutoSave Plugin
Autosave is a feature where the application saves your file automatically every few seconds as you work. Camunda Modeler
does not have an Autsave feature, and hence this plugin will save you valueable time. 

**Download Plugin**: [https://github.com/pinussilvestrus/camunda-modeler-autosave-plugin](https://github.com/pinussilvestrus/camunda-modeler-autosave-plugin)

![Camunda Modeler Plugin Autosave](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-autosave.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - AutoSave
{:.figcaption}

### 2. Property Info Plugin
The Property Info plugin provides an overview of which properties are set per BPMN shape. There are several badges that
illustrate whether Execution Listeners, Task Listeners, Extensions, Input & Output parameters or Field Injections properties are set.

**Download Plugin**: [https://github.com/umb/camunda-modeler-property-info-plugin](https://github.com/umb/camunda-modeler-property-info-plugin)

![Camunda Modeler Plugin Property Info](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-property-info.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - Property Info
{:.figcaption}

### 3. BPMN Lint Plugin
The BPMN Lint plugin allows you to validate your BPMN diagram against a set of configurable rules. This plugin uses 
the recommended bpmnlint and Camunda rules. The plugin evaluates rules like, "Conditional Flows", "End Event Required", 
"Fake Joins", "Label Required", etc..

**Download Plugin**: [https://github.com/camunda/camunda-modeler-linter-plugin](https://github.com/camunda/camunda-modeler-linter-plugin)

![Camunda Modeler Plugin BPMN Lint](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-bpmn-lint.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - BPMN Lint
{:.figcaption}

### 4. Tooltips Plugin
The Tooltip plugin adds tooltips to the various BPMN elements. For example, the tooltip displays the properties and values 
of the BusinessRuleTask once the mouse hovers over the BPMN activity. The properties include "Implementation", "Decision", 
"Binding", "Result Variable", etc. It also displays information about conditional sequence flows if the mouse hovers over 
an Exclusive Gateway. 

**Download Plugin**: [https://github.com/viadee/camunda-modeler-tooltip-plugin](https://github.com/viadee/camunda-modeler-tooltip-plugin)

![Camunda Modeler Plugin Tooltip](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-tooltip.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - Tooltip
{:.figcaption}

### 5. Token Simulation Plugin
The Token Simulation plugin allows you to simulate the tokens and how they will flow through the BPMN process. The plugin 
beautifully simulates the splitting of a token at the parallel gateway, and also allows you to spawn new tokens at the
boundary events.

**Download Plugin**: [https://github.com/bpmn-io/bpmn-js-token-simulation-plugin](https://github.com/bpmn-io/bpmn-js-token-simulation-plugin)

![Camunda Modeler Plugin Token Simulation](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-token-simulation.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - Token Simulation
{:.figcaption}

### 6. Color Picker Plugin
The Color Picker plugin allows you to change the color of any of the BPMN elements.

**Download Plugin**: [https://github.com/camunda-community-hub/camunda-modeler-plugin-color-picker](https://github.com/camunda-community-hub/camunda-modeler-plugin-color-picker)
![Camunda Modeler Plugin Color Picker](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-color-picker.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - Color Picker
{:.figcaption}

### 7. Transaction Boundaries Plugin
The Transaction Boundaries plugin visualizes the transaction boundaries on the BPMN process model. This is set by the 
Asynchronous Continuation properties (Asynchronous Before & Asynchronous After).

**Download Plugin**: [https://github.com/camunda/camunda-modeler-plugins/tree/master/camunda-transaction-boundaries-plugin](https://github.com/camunda/camunda-modeler-plugins/tree/master/camunda-transaction-boundaries-plugin)
![Camunda Modeler Plugin Transaction Boundaries](/assets/images/posts/camunda-modeler-plugins/camunda-modeler-plugin-transaction-boundaries.png){:.lead width="800" height="100" loading="lazy"}

Camunda Modeler Plugin - Token Simulation
{:.figcaption}

## List of Other Plugins
The list of Camunda Modeler plugins is growing by the day. Here are some more useful plugins:

* [Camunda Platform to Cloud Migration Plugin](https://github.com/camunda-community-hub/camunda-platform-to-cloud-migration)
* [User Task Generated Form Preview Plugin](https://github.com/camunda-community-hub/camunda-modeler-plugin-usertask-generatedform-preview)
* [Reduced Palette Plugin](https://github.com/camunda-community-hub/camunda-modeler-plugin-reduced-palette)
* [Rename Technical IDs Plugin](https://github.com/camunda-community-hub/camunda-modeler-plugin-rename-technical-ids)
* [Embedded Comments Plugin](https://github.com/camunda/camunda-modeler-plugins/tree/master/bpmn-js-plugin-embedded-comments)
* [Internationalisation Plugin](https://github.com/FlowSquad/camunda-modeler-i18n-plugin)
* [Multi-Diagram Plugin](https://github.com/sharedchains/camunda-modeler-plugin-multidiagram)
* [Process I/O Specification Plugin](https://github.com/camunda/camunda-modeler-process-io-specification-plugin)
* [DMN Testing Plugin](https://github.com/bpmn-io/dmn-testing-plugin)
* [DMN Excel Import Plugin](https://github.com/pinussilvestrus/camunda-modeler-excel-import-plugin)
* [WYSIWYG Documentation Plugin](https://github.com/sharedchains/camunda-wysiwyg-documentation)

## Camunda Modeler Plugin Templates 
If you interested in creating your own Camunda Modeler Plugin, use the following as starting point:
* [BPMN-JS Plugin Example](https://github.com/camunda/camunda-modeler-plugins/tree/master/bpmn-js-plugin-example)
* [DMN-JS Plugin Example](https://github.com/camunda/camunda-modeler-plugins/tree/master/dmn-js-plugin-example)
* [BPMN-JS Moddle Extension Plugin Example](https://github.com/camunda/camunda-modeler-plugins/tree/master/bpmn-js-plugin-moddle-extension-example)
* [Menu Plugin Example](https://github.com/camunda/camunda-modeler-plugins/tree/master/menu-plugin-example)
* [Style Plugin Example](https://github.com/camunda/camunda-modeler-plugins/tree/master/style-plugin-example)

See the Camunda Modeler Plugin [documentation](https://github.com/camunda/camunda-modeler/tree/master/docs/plugins) for more information.

## Finally 
The Camunda community is growing and more Modeler plugins are greated everyday. This article will be updated as new plugins are created. Follow me on any of the different social media platforms and feel free to leave comments.

