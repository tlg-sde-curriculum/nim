---
title: Model
nav_order: 3
parent: "Separation of concerns"
---

{% include abbreviations.md %}

# {{ page.title }}
{:.no_toc}

## Overview

The model classes are responsible for maintaining the internal state of the game (as well as the tally of wins/losses over a series of games), with suitable methods for recording moves to update the state, and accessor methods to make a subset of that state information available to the view and controller classes.


## Classes

All of these classes should be in the `com.tlglearning.nim.model` package. Optionally, students should consider whether any of these classes can and should be made inner or static nested classes within others.

### `Game`

Encapsulates a single game, composed of a `List<Pile>` and a `State`. Its fields must not be modifiable directly by consumers, nor should mutator methods be provided; instead, a `play(Pile, int)` method must be implemented to apply a specified move to the game and update its state.

In addition to accessor methods for the `List<Pile>` and a `State`, an `isFinished()` method should be implemented to allow a consumer (e.g. a controller class) to check the completion state of the game following each move.

### `Pile`

This class represents a single pile of markers/tokens. Initially, all of these are available for removal (via a `remove(int)` method, which should only accessible from inside the `model` package); as they are removed, the number removed and the number remaining must be available via accessors, so that a view can construct a suitable representation.

## UML diagram

![Model class diagram]({{ "/assets/images/model.svg" | relative_url }})