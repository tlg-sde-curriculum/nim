---
title: Separation of concerns
nav_order: 3
has_children: true
---

{% include abbreviations.md %}

# {{ page.title }}
{:.no_toc}

## Overview

Implementation of the _Nim_ game program will employ a separation of concerns between groups of classes and interfaces, with each group in its own package(s). More specifically, a simplified _Model-View-Controller_ (_MVC_) approach will be used.

Because the game is to implemented for text-mode play, all user interaction will be synchronous; thus, the concerns handled by the view will be limited to constructing `String` representations of the piles of objects, as well as constructing `String` user prompts. Receiving and processing the user input will be handled by the conroller classes, invoking methods on view classes as appropriate. (We might characterize this as a _passive-view_ variation of MVC.)
In addition to packages for each of model, view, and controller, another package will be used to implement the computer's strategy for play.

## UML class diagram

This is a diagram showing the classes for a possible implementation of the game. While we suggest that an implementor follow this diagram fairly closely, many details are left up to the implementor. (For example, note that the diagram shows no private fields.)

![Model class diagram]({{ "/assets/images/model.svg" | relative_url }})