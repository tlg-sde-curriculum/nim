---
title: View
nav_order: 2
parent: "Separation of concerns"
---

{% include abbreviations.md %}

# {{ page.title }}
{:.no_toc}

<details markdown="block">
  <summary>Contents</summary>
* TOC
{:toc}
</details>

## Overview

The view classes are responsible for constructing `String` representations of the piles and current state of a game, moves made by the players, and the tally of wins and losses in a multi-game session.

## Classes

All of these classes should be in the `com.tlglearning.nim.model` package. Optionally, the implementor should consider whether any of these classes can and should be made inner or static nested classes within others.

### `GameView`

### `PileView`

### `TallyView`

## UML class diagram

![View class diagram]({{ "/assets/images/view.svg" | relative_url }})