---
title: "Theoretical Computer Science Cheat Sheet"
source: "https://www.arnevogel.com/theoretical-computer-science-cheat-sheet/?utm_source=chatgpt.com"
author:
  - "[[Arne Vogel]]"
published:
created: 2026-01-19
description:
tags:
  - "clippings"
---
Jan 1, 2018 • Arne Vogel

## Automata and Formal Languages

### Formal Languages

An **alphabet** Σ $Σ$ is a finite set of symbols. For example { 0,1 } ${0,1}$ is an alphabet and { a,b,c,d } ${a,b,c,d}$ is an alphabet. An **word** is a finite set of symbols from an alphabet Σ $Σ$. One word for the alphabet { a,b,c,d } ${a,b,c,d}$ would be a b c $abc$ and another one would be a a a b $aaab$. The length of a word w $w$ is defined as the number of symbols it has. So the length of the word 01010 $01010$ from the alphabet { 0,1 } ${0,1}$ would be 5 $5$. Every alphabet contains the **empty word**. The empty word is the word with size 0 $0$. The set of all words that can be created from an alphabet is Σ ∗ $Σ∗$.

Words can be combined. Combining word w \= 010 $w=010$ and word v \= 101 $v=101$ creates a new word w v \= 010101 $wv=010101$. Combining any for with the empty word results in the same word: w ε \= w \= ε w $wε=w=εw$.

Σ ∗ $Σ∗$ is created with the *Kleene Star* algorithm. The Kleene Star algorithm creates every possible word for an alphabet Σ $Σ$.

#### Kleene Star Algorithm

Given an alphabet V $V$:

V 0 \= { ε } 
$$
V0={ε}
$$
 V 1 \= V 
$$
V1=V
$$

now recursively define for all i > 0:

V i + 1 \= { w v | w ∈ V i,v ∈ V } 
$$
Vi+1={wv|w∈Vi,v∈V}
$$

Example: V \= { a,b } $V={a,b}$ then V 0 \= { ε } $V0={ε}$, V 1 \= { a,b } $V1={a,b}$, V 2 \= { a,b,a a,a b,b a,b b } $V2={a,b,aa,ab,ba,bb}$,…

#### Formal Language

A **Formal language** *L* over an alphabet Σ $Σ$, is a subset of Σ ∗ $Σ∗$.

Example: Σ \= { a,b,c } $Σ={a,b,c}$. One viable language would be L 1 \= { a a,a b,b b,b c,a b c,c c } $L1={aa,ab,bb,bc,abc,cc}$. L 1 $L1$ has 6 $6$ elements. Another language for the same alphabet could be L 2 \= { a n b n c n | n ∈ N } $L2={anbncn|n∈N}$. L 1 $L1$ is defined by it’s elements. L 2 $L2$ on the other hand is defined by how to build words that are in L 2 $L2$. L 2 \= { a b c,a a b b c c,a a a b b b c c c,… } $L2={abc,aabbcc,aaabbbccc,…}$.

## Automata

### Deterministic Finite Automaton DFA

DFA’s are used to determine if a word w $w$ is element of an language L $L$. A deterministic finite automaton is defined as A \= (Q,,Σ,,δ,,q 0,,F) $A=(Q,,Σ,,δ,,q0,,F)$.

- Q $Q$ is the finite number of states of the DFA
- Σ $Σ$ is an alphabet
- δ $δ$ is a transition function δ:Q × Σ → Q $δ:Q×Σ→Q$
- q 0 $q0$ is the start state of the DFA q 0 ∈ Q $q0∈Q$
- F $F$ is a set of final states F ⊆ Q $F⊆Q$

Example:

![DFA](https://www.arnevogel.com/images/theoretical-computer-science-cheat-sheet/DFA.svg)

This DFA accepts binary numbers that are multiples of 3. Q \= { S 0,S 1,S 2 } $Q={S0,S1,S2}$, Σ \= { 0,1 } $Σ={0,1}$,

δ \= $δ=$

|  | 0 $0$ | 1 $1$ |
| --- | --- | --- |
| **→ S ∗ 0 $→S0∗$** | S 0 $S0$ | S 1 $S1$ |
| **S 1 $S1$** | S 2 $S2$ | S 0 $S0$ |
| **S 2 $S2$** | S 1 $S1$ | S 2 $S2$ |

q 0 \= S 0 $q0=S0$, F \= { S 0 } $F={S0}$.

In the transfer table a state with → $→$ in front it means its a start state. The other symbol ∗ $∗$ means its a final state.

### Nondeterministic Finite Automaton NFA

In a NFA there can be states where you can choose from different options to “move” through the NFA. This makes the NFA non-deterministic because the “path” is not set in stone. Every DFA is automatically a NFA but not every NFA is a DFA.

![NFA](https://www.arnevogel.com/images/theoretical-computer-science-cheat-sheet/NFA.svg)

In this example you can choose to stay in S 0 $S0$ when you read a 1 $1$ or you can choose to move to S 1 $S1$. This means the NFA only accepts words that end with a 1 $1$.

The transfer table for the NFA:

|  | 0 | 1 |
| --- | --- | --- |
| → S 0 $→S0$ | S 0 $S0$ | { S 0,S 1 } ${S0,S1}$ |
| S ∗ 1 $S1∗$ | ∅ $∅$ | ∅ $∅$ |

### Converting NFA to DFA

Take the transfer table from the NFA and take the start state and look where it leads for each symbol and make a new set from them. If the set contains a final state also make the new state a final state. Repeat that for each new set until no set wasn’t handled.

If you want you can rename the sets afterwards.

Example with the NFA from above:

|  | 0 $0$ | 1 $1$ |
| --- | --- | --- |
| → S 0 $→S0$ | S 0 $S0$ | { S 0,S 1 } ${S0,S1}$ |
| { S 0,S 1 } ∗ ${S0,S1}∗$ | S 0 $S0$ | { S 0,S 1 } ${S0,S1}$ |

The resulting DFA from the NFA:

![DNA from an NFA](https://www.arnevogel.com/images/theoretical-computer-science-cheat-sheet/DFAfromNFA.svg)