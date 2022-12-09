---
title: Rules
nav_order: 1
parent: "Game of Nim"
---

{% include abbreviations.md %}

# {{ page.title }}
{:.no_toc}

<details markdown="block">
  <summary>Contents</summary>
* TOC
{:toc}
</details>

## Setup

* Two players.

* One or more _piles_ (or _heaps_), each holding a positive quantity of items. Played with pencil and paper, the items are typically tally marks (which can be crossed out); played with physical objects, the items in each pile are matchsticks, toothpicks, stones, etc.

* The player moving first may be determined by agreement between the players or selected at random. If multiple games are played in sequence, players typically alternate moving first.

## Play

* Alternating turns, each player removes (_nims_) a positive number of items from a single pile. Once a given pile is exhausted---i.e. when all items have been removed from the pile---further removal from that pile is not possible. 

* Play ends when all piles are exhausted---i.e. when there are no items remaining to be removed.

## Winning

* In the _mis&egrave;re_ variation, the player who removes the last item loses the game. This is the most commonly played form of Nim.

* In the normal-play variation, the player who removes the last item wins the game. This is the variation for which the optimal strategy is described below. (The optimal strategy for the mis&egrave;re variation is almost identical, changing only when the normal-play optimal move would remove all remaining items, or when the normal-play optimal move would leave only piles with single items.)
