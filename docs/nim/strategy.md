---
title: Strategy
nav_order: 2
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

## Optimal strategy

The optimal strategy for normal play is to end each move so that the remaining items in all piles form a _nim sum_ of zero. The nim sum is the _binary digital sum without carries_ of the numbers of remaining items in all piles, or the _bitwise exclusive OR_ of those numbers. 

### Bitwise XOR

#### Computation in concept

The _bitwise exclusive OR_, or _bitwise XOR_, of two or more integer operands is indicated in mathematical notation by the $\oplus$ operator, and is computed by the following steps:

1. Express all of the operands in base-2 form, left-padding them with 0 (zero) as necessary so that all are the same length. (The result will also be of this length.)

2. For each digit position, compute the sum of the digits in that position in all operands, to obtain the digit in the same position in the result:

    * If the sum is even (i.e. divisible by 2),

        * the digit in the corresponding position in the result is 0;
        
        otherwise,

        * the digit in the corresponding position in the result is 1.

For example, to compute the nim sum of 3, 5, and 7, we start with the base-2 representations of those values:

$$
\begin{aligned}
3_{10} &= 011_2 \\
5_{10} &= 101_2 \\
7_{10} &= 111_2 \\
\end{aligned}
$$ 

Now, we examine each of the digits sums in the base-2 representation. Since the digits in the right-most position sum to 3, and this is odd, the result will have 1 in the right-most position. However, in both of the positions to the left of that, the sum is 2, which is even, for a result of 0 in both of those two positions. Thus, we obtain a result of $001_2$, or 1.

Note that as can be inferred from the above, the associative property holds for bitwise XOR---that is, $A \oplus B \oplus C = (A \oplus B) \oplus C = A \oplus (B \oplus C)$. This can be extended for any number of terms:

$$
A_1 \oplus A_2 \oplus A_3 \oplus \ldots \oplus A_n = (\ldots ((A_1 \oplus A_2) \oplus A_3) \oplus \ldots ) \oplus A_n)
$$

In other words, the bitwise XOR of any number of terms can be computed by taking the bitwise XOR of the first two, then taking the bitwise XOR of that first result with the third term, and so on.

#### Computation in Java

Fortunately, for an implementation in Java (or any C-derived language), the bitwise XOR is a simple matter of using the `^` operator. For example, the expression `3 ^ 5 ^ 7` computes the bitwise XOR (or nim sum) of those three values. (Verify that computation in JShell.)

### Move selection algorithm

The optimal strategy for selecting a move in normal play can be expressed in pseudocode by this algorithm:

#### Given

* Let $n$ be the number of piles (heaps).

* Let $P$ be the quantities in the $n$ piles---that is, $p_0$ is the number remaining in pile $0$, $p_1$ the number remaining in pile $1$, and so on.

#### Operators

In addition to the usual arithmetic operators, the steps below use two more that may be unfamiliar to you:

| Operator | Meaning |
|:--------:|:--------|
| $\oplus$ | Exclusive XOR (as described above). |
| $\gets$ | Assignment (like `=` in C-derived languages, `:=` in Pascal-derived languages, etc.). |

#### Steps

1. Let $M \gets (0, 0, \ldots, 0)$.

    ($M$ is an ordered sequence of $n$ candidate moves, $m_0, m_1, \ldots, m_{n - 1}$. Initially, all values in the sequence are equal to $0$.) 

2. Let $S \gets 0$.

    ($S$ will eventually hold the nim sum of $P$; initially, it is assigned the value $0$.) 

3. For each $p_i$ in $P$:

    > 1. $S \gets S \oplus p_i$.
    >
    (When this step is complete, $S$ is the nim sum of $P$.)

4. If $S \ne 0$:

    > 1. For each $p_i$ in $P$:
    >
    >    > 1. If $S \oplus p_i \le p_i$:
    >    >
    >    >    > *  $m_i = p_i - (S \oplus p_i)$.
    >
    > 2. Select $j$ at random, such that $m_j > 0$.
    >
    >    (That is, select a random non-zero element of $M$.)
    >
    > 3. The optimal move is to remove the quantity $m_j$ from pile $j$.
       
    otherwise:

    > 4. No optimal move exists. Any move will permit the other play to make an optimal move in turn; thus, a move may be selected at random, or some other heuristic may be used. 

