---
layout: post
title: "How to Uninstall Java on MacOS"
author: andre
categories: [ java-general ]
tags: [java, macOS]
image: /assets/images/feature-images/feature-image-java.png
description: This post explains and guide you on how to uninstall Java on your macOS. To uninstall Java from your macOS is a manual process since there is no automatic uninstaller available for the numerous JDK distributions.
comments: true
---
- Table of Contents
{:toc .large-only}

To uninstall Java from your macOS is a manual process since there is no automatic uninstaller available for the numerous 
JDK distributions.   

You would require Administrator privileges to execute the remove commands in the terminal either as root or by using the 
sudo tool.

Always be careful when using the remove command and make sure you understand exactly what files and directory structures
it will delete before running it.

## Determine the Java JDK version(s) 
First determine what version of the Oracle JDK you have by running the following commands:
```bash
# Print the Java version to the output stream and exit
$ java -version

# Print the path to a Java home directory from the current user's settings
$ /usr/libexec/java_home -V

# Print the list of Java VirtualMachines currently installed.
$ ls -la /Library/Java/JavaVirtualMachines/
```

## Uninstall Java Virtual Machine (JVM) 
You can either remove a specific version of the JDK or all of them, depending on the setup of your Java environment on 
your macOS. Since these commands will remove the files and directories from your macOS operating system, please make 
sure you delete the correct version.   

```bash
# Run this command to remove a specific JDK version
$ sudo rm -rf /Library/Java/JavaVirtualMachines/jdk<version>.jdk

# Run this command to remove all the JDK versions
$ sudo rm -rf /Library/Java/JavaVirtualMachines/
```

## Remove the Java Control Panel
The Java Control Panel can be found by clicking on the Apple icon in the upper left corner of the screen. Select 
`System Preferences` and select the Java icon to access the Java Control Panel.

The Java Control Panel contains information about the Java version, network settings, java runtime environment settings, 
etc... 

To remove the Java Control Panel use the following command:
```bash
# Run these commands if you want to remove plugins
$ sudo rm -rf /Library/PreferencePanes/JavaControlPanel.prefPane
```

## Remove Java Plugins & Preferences 
There are several other Java plugins, helpers and preference lists that are optional for you to remove.

```bash
$ sudo rm -rf /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin
$ sudo rm -rf /Library/LaunchAgents/com.oracle.java.Java-Updater.plist
$ sudo rm -rf /Library/PrivilegedHelperTools/com.oracle.java.JavaUpdateHelper
$ sudo rm -rf /Library/LaunchDaemons/com.oracle.java.Helper-Tool.plist
$ sudo rm -rf /Library/Preferences/com.oracle.java.Helper-Tool.plist
```

## Summary
Congratulations! You have successfully uninstall Java from you macOS operating system. Follow me on any of the different social media platforms and feel free to leave comments.