---
title: Model
nav_order: 1
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

The model classes are responsible for maintaining the internal state of the game (as well as the tally of wins/losses over a series of games), with suitable methods for recording moves to update the state, and accessor methods to make a subset of that state information available to the view and controller classes.

## Classes

All of these classes should be in the `com.tlglearning.nim.model` package. Optionally, the implementor should consider whether any of these classes can and should be made inner or static nested classes within others.

### `State`

Represents the current state of a single game: which player's turn is it to move, or---if the game is completed---which player won. Thus, four enumerated values must be declared to represent the possible states, e.g.: `PLAYER_1_MOVE`, `PLAYER_2_MOVE`, `PLAYER_1_WIN`, `PLAYER_2_WIN`.  

Beyond defining the possible states of the game, this enum must also implement finite-state machine behavior: It must include fields and methods sufficient to allow a consumer to know whether a given state is terminal (`isTerminal()`), which state would result from a winning move in the given state (`nextWinState()`), and which state would result from a non-winning move in the given state (`nextMoveState()`). 

### `Pile`

This class represents a single pile of markers or tokens. Initially, all of these are available for removal (via a `remove(int)` method, which should only accessible from inside the `model` package). As markers are removed, this class needs to keep track of how many have been removed and how many remain, making this information available via accessor methods. In addition, a `boolean isEmpty()` method should be provided for convenience: this method must return `true` if there are no markers remaining (i.e. all markers have been removed).

The constructor for this class must use a parameter that allows invocation with a specified initial quantity remaining.

### `Game`

Encapsulates a single game, composed of (minimally) a `List<Pile>` and a `State`. Its fields must not be modifiable directly by consumers, nor should mutator methods be provided; instead, a `play(Pile, int)` method must be implemented to apply a specified move to the game and update its state.

In addition to accessor methods for the `List<Pile>` and a `State`, an `isFinished()` convenience method should be implemented to allow a consumer (e.g. a controller class) to check the completion state of the game following each move.

This class must provide a constructor that supports initializing an instance in a given non-terminal state and with specified initial pile sizes---all specifiable via parameters.

### `Move`

Instances of this class serve to package the information about a move in a form that usable by the `Game` class, as well as the `MoveView` class; they are not retained by `Game` after the state is updated as a result of the move, nor by the `MoveView` class after a `String` representation of the move is consructed.

For the purpose described above, the class encapsulates a 1-based pile number (used by `MoveView`), a reference to the corresponding `Pile` (used by `Game`), and the quantity to be removed from the pile (used by both `MoveView` and `Game`). 

Instances of this class are instantiated by a `Strategy` implementation (for moves made by the computer) and by `SessionController.GameController` (for moves made by the human player).

### `Tally`

This class is precisely what it sounds like: It encapsulates a tally of wins and losses, with `win()` and `lose()` methods to increment those tallies, and accessors to make the tallies available to consumers.

## UML class diagram

The diagram below shows constructors and methods, including accessors. However, it does not show any private fields; it's up to the implementor to decide (using the diagram along with the summaries above) what fields will be needed in order to support the required functionality, and whether any given accessor method will return a field value or the result of a more complex computation. 

For example, in the `Pile` class, it would probably make sense to have `remaining` and `removed` fields of the `int` type; `getRemaining()` and `getRemoved()` would simply return the values of such fields. On the other hand, the `isEmpty()` method doesn't necessarily require a corresponding `boolean empty` field; instead, it could return the `boolean` result of the `remaining == 0` expression.

The open lock icon is used to indicate that the corresponding constructor, method, or field is public; a small open circle indicates the package-private access level.

![Model class diagram]({{ "/assets/images/model.svg" | relative_url }})