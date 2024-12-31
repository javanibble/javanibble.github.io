---
layout: post
title: "Vim Essentials"
author: andre
categories: [ vi ]
tags: [vi, vim]
image: /assets/images/feature-images/feature-image-keyboard.jpg
description: This post provides a quick reference to the keyboard shortcuts and commands for the Vim application.
comments: true
---

- Table of Contents
{:toc .large-only}

## What is VI and VIM?
> Vim stands for Vi IMproved and Vi is short for visual. It used to be Vi IMitation, but there are so many improvements that a name change was appropriate.  Vim is a powerful text editor which includes almost all the commands from the Unix program "Vi" and a lot of new ones.  It is very useful for editing programs and other plain text. All commands are given with the keyboard. This has the advantage that you can keep your fingers on the keyboard and your eyes on the screen.

## Vim Modes
Vim has seven basic modes:
* **Normal Mode**: In Normal mode you can enter all the normal editor commands. If you start the editor you are in this mode. This is also known as **Command Mode**.
* **Insert Mode**: In Insert mode the text you type is inserted into the buffer. If the 'showmode' option is on `-- INSERT --` is shown at the bottom of the window.
* **Command-line Mode**: In Command-line mode (also called Cmdline mode) you can enter one line of text at the bottom of the window. Command-line mode is used to enter Ex commands (':'), search patterns ('/' and '?'), and filter commands ('!'). This is also known as **Line Mode** or **Last Line Mode**.
* **Visual Mode**: Visual mode is a flexible and easy way to select a piece of text for an operator.  It is the only way to select a block of text. This is like Normal mode, but the movement commands extend a highlighted area. When a non-movement command is used, it is executed for the highlighted area. If the 'showmode' option is on `-- VISUAL --` is shown at the bottom of the window.
* **Select Mode**: Select mode looks like Visual mode, but the commands accepted are quite different. This looks most like the MS-Windows selection mode. Typing a printable character deletes the selection and starts Insert mode. If the 'showmode' option is on `-- SELECT --` is shown at the bottom of the window. 
* **Ex Mode**: Like Command-line mode, but after entering a command you remain in Ex mode. Very limited editing of the command line.
* **Terminal-Job Mode**: Interacting with a job in a terminal window.  Typed keys go to the job and the job output is displayed in the terminal window.  

## Vim Help
The following set of keyboard shortcuts are related to the terminal window and the multiple tabs within the terminal window.

| Command |  Description |
|---------|--------------|
| :help or :h | Open a new window and display the help file in read-only mode. | 
| :help [subject] | Access help from within vim on specific subject. E.g. `:help modes` |
| :help [command] | Access help from within vim on specific command. E.g. `:help :help`, `:help ^f` |
| Ctrl-o | Move back to previous section in the help window. |
| Ctrl-i | Move forward to the next section in the help window. |
| Ctrl-] | Jump to the definition of the keyword under the cursor. |
| Ctrl-w Ctrl-w| Go to the next window. |
| :h :q Ctrl-d | List all the commands starting with q. Press TAB to iterate through list.|
| :q | Quit the current window. |
{:.stretch-table}

Vim Help Commands
{:.figcaption}

## Navigation Commands (Motions)
The following set of commands can only be issued in Normal Mode (Command Mode).

| Command |  Description |
|---------|--------------|
| `h`, `j`, `k`, `l` | Move the cursor left, down, up, right |
| `Ctrl-f` | Move the cursor forward in the file. It is the same as the "page down" operation. |
| `Ctrl-b` | Move the cursor backward in the file. It is the same as the "page up" operation. |
| `H` | Move the cursor to the top line of the current window. (High) |
| `M` | Move the cursor to the middle line of the current window. (Middle) |
| `L` | Move the cursor to the bottom line of the current window. (Low) |
| `W` | Move the cursor forward by word. (Using whitespace as word boundaries) |
| `B` | Move the cursor backward by word. (Using whitespace as word boundaries) |
| `w` | Move the cursor forward by word. (Using whitespace, punctuation as word boundaries) |
| `b` | Move the cursor  backward by word. (Using whitespace, punctuation as word boundaries) |
| `0` | Move the cursor to the beginning of the current line. |
| `^` | Move the cursor to the first word in the current line. |
| `$` | Move the cursor to the end of the current line. |
| `1gg` or `gg` | Go to the beginning of the file. |
| `$G` or `G` | Go to the last line of the file. |
| `<line_number>gg` or `<line_number>G` | Go to a specific line number. |
| :<line_number>: | Go to a specific line number. |
{:.stretch-table}


## Delete Text
The following set of commands can only be issued in the Normal Mode (Command Mode).

| Command |  Description |
|---------|--------------|
| `x` | Delete characters under and after the cursor. |
| `3x`| Delete 3 characters under and after the cursor. |
| `X` | Delete characters before the cursor. |
| `3X`| Delete 3 characters before the cursor. |
| `dw` | Delete the current word at the cursor. |
| `dd` | Delete the current line at the cursor. |
| `5dd` | Delete 5 lines |
| `d$` | Delete to the end of the line from the cursor. |
| `d0` | Delete to the beginning of the line from the cursor. |
| `dh` | Delete characters before the cursor. |
| `dl` | Delete characters under and after the cursor. |
| `dj` | Delete the current line and the line below of the cursor. |
| `dk` | Delete the current line and the line above of the cursor. |


## Summary
Congratulations! You have completed the post about the keyboard shortcuts and commands of VIM. Follow me on any of the different social media platforms and feel free to leave comments.

