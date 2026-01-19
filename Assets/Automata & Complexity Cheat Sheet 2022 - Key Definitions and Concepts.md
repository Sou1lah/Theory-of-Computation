
# Automata & Complexity 



## Automata & Complexity Cheat Sheet

*Based on notes by Jörg Endrullis*


---

## 1. Regular Languages


### 1.1 Deterministic Finite Automata


**Definition:** A deterministic finite automaton (DFA) is a tuple $(Q, \Sigma, \delta, q_0, F)$ consisting of:
- a finite set $Q$ of states
- a finite input alphabet $\Sigma$
- a transition function $\delta: Q \times \Sigma \to Q$
- a starting state $q_0 \in Q$
- a set $F \subseteq Q$ of final states

**Product construction:** To construct a DFA $N$ that runs two DFAs $M_1$ and $M_2$ in parallel:
Let $M_1 = (Q_1, \Sigma, \delta_1, q_{0,1}, F_1)$ and $M_2 = (Q_2, \Sigma, \delta_2, q_{0,2}, F_2)$.
Define $N = (Q, \Sigma, \delta, q_0, F)$ where:
- $Q = Q_1 \times Q_2 = \{ (q_1, q_2) \mid q_1 \in Q_1, q_2 \in Q_2 \}$
- $\delta((q_1, q_2), a) = (\delta_1(q_1, a), \delta_2(q_2, a))$
- $q_0 = (q_{0,1}, q_{0,2})$
- $F = \{ (q_1, q_2) \in Q \mid q_1 \in F_1 \text{ or } q_2 \in F_2 \}$
Then $L(N) = L(M_1) \cup L(M_2) = L_1 \cup L_2$.


### 1.2 Nondeterministic Finite Automata


We use $2^Q$ to denote the set of all subsets of $Q$.

**Definition:** A nondeterministic finite automaton (NFA) is a tuple $(Q, \Sigma, \delta, S, F)$ consisting of:
- a finite set $Q$ of states
- a finite input alphabet $\Sigma$
- a transition function $\delta: Q \times (\Sigma \cup \{\lambda\}) \to 2^Q$
- a set $S \subseteq Q$ of starting states
- a set $F \subseteq Q$ of final states

**Powerset construction:** Given an NFA $M = (Q, \Sigma, \delta, S, F)$, construct a DFA $N = (Q', \Sigma, \delta', q'_0, F')$ where:
- $Q' = 2^Q = \{ X \mid X \subseteq Q \}$
- $\delta'(X, a) = \{ q' \in Q \mid q \xrightarrow{a} q' \text{ for some } q \in X \}$
- $q'_0 = \{ q' \in Q \mid q \xrightarrow{\lambda} q' \text{ for some } q \in S \}$
- $F' = \{ X \subseteq Q \mid X \cap F \neq \emptyset \}$
Then $L(N) = L(M)$.




### 1.3 Grammars

Definition. A grammar G = (V, T, S, P ) consists of finite set V of non- terminals (or variables), finite set T of terminals, a start symbol S ∈ V, finite set P of production rules x → y where x ∈ (V ∪ T )+ contains at least one symbol from V, and y ∈ (V ∪ T )∗.


### 1.4 Regular Expressions


A regular expression is syntax describing a language. Over an alphabet $\Sigma$:
- $\emptyset$ is a regular expression
- $\lambda$ is a regular expression
- $a$ is a regular expression for every $a \in \Sigma$
- $r_1 + r_2$ is a regular expression for all regular expressions $r_1$ and $r_2$
- $r_1 \cdot r_2$ is a regular expression for all regular expressions $r_1$ and $r_2$
- $r^*$ is a regular expression for all regular expressions $r$

Each regular expression $r$ defines a language $L(r)$:
- $L(\emptyset) = \emptyset$
- $L(r_1 + r_2) = L(r_1) \cup L(r_2)$
- $L(\lambda) = \{ \lambda \}$
- $L(r_1 \cdot r_2) = L(r_1)L(r_2)$
- $L(a) = \{ a \}$ for $a \in \Sigma$
- $L(r^*) = L(r)^*$

**From regular expressions to NFAs:** For every regular expression $r$, we build an NFA $M$ such that $L(M) = L(r)$, with one final and one (different) starting state. We construct $M$ by induction on $r$ as follows:

![[image-6.png]]



### 1.5 String Matching (Thompson)


**Problem:** Given a word $u$ and a regular expression $r$, does $u$ contain a subword in $L(r)$?

**Construction:**
1. Transform the regular expression $\Sigma^* \cdot r$ into an NFA.
2. Compute the path of $u$ in the corresponding DFA on-the-fly.
3. Terminate as soon as a final state is reached.


### 1.6 Minimal DFAs


**Construction:**
1. Remove all unreachable states from $M$.
2. Partition $Q$ into indistinguishable states:
	- Initial partition: $\{ Q \setminus F, F \}$
	- If there are partitions $R$ and $S$ such that $\delta(q, a) \in S$ and $\delta(q', a) \notin S$ for some $a \in \Sigma$ and $q, q' \in R$, split $R$ accordingly.
	- Repeat until no more splits are possible.
3. The resulting partitioning gives the states of the minimal DFA $\hat{M}$.
	- Transitions: $Q_i \xrightarrow{a} Q_j$ iff $q \xrightarrow{a} q'$ for some $q \in Q_i, q' \in Q_j$
	- The starting state is the set containing $q_0$; final states are those containing elements of $F$.


### 1.7 Pumping Lemma for Regular Languages


**Theorem (Pumping Lemma):**
Let $L$ be a regular language. There exists $m > 0$ such that every $w \in L$ with $|w| \geq m$ can be written as $w = xyz$ with $|xy| \leq m$, $|y| \geq 1$, and $xy^iz \in L$ for every $i \geq 0$.

**Remark:** To prove that a language $L$ is not regular, show that the pumping property does not hold for every $m$ and every possible decomposition $w = xyz$.


---

## 2. Context-Free Languages


### 2.1 Chomsky Normal Form


**Definition:** A variable $A$ is called erasable if $A \Rightarrow^+ \lambda$.


**Construction (Removal of lambda productions):**

- Determine all erasable variables.
- For every rule A → xBy with B ⇒∗ λ, add a rule A → xy.
- Remove all λ-production rules.

The resulting grammar generates the language L \\ { λ }.


**Definition:** A rule $A \to B$ is called a unit production rule (here $B \in V$).


**Construction (Removal of unit productions):** First, remove all $\lambda$-rules.

- Determine all pairs A ̸= B with A ⇒+ B.
- Whenever A ⇒+ B and B → y is a rule, add a rule A → y.
- Remove all unit production rules.

The resulting grammar generates the language L \\ { λ }.



(ii) useless for a context-free grammar if there exists no derivation of the form

S ⇒∗ uAv ⇒+ w with w ∈ T ∗.

Construction (Removing non-productive variables). We determine all produc- tive variables:

- If A → y is a rule and all variables in y are productive, then A is productive.

Afterwards, we remove all rules that contain a non-productive variable.

Construction (Removing non-reachable variables). We determine all reach- able variables as follows:

- S is reachable.
- If A → y and A is reachable, then so are all variables in y.

Afterwards, we remove all rules that contain a non-reachable variable.

Construction (Removing useless variables). First, remove all rules that con- tain a non-productive variable. Second, remove all rules that contain a non- reachable variable. A variable is useful if it is in one of the remaining rules (and otherwise useless).

Definition. We consider the first terminal letters derivable from a word:

First(w) = { a ∈ T | w ⇒∗ a... } ∪ { λ | w ⇒∗ λ }

Construction (First). Let PreFirst(w) be the smallest set such that:

- w ∈ PreFirst(w)
- a ∈ PreFirst(w) if av ∈ PreFirst(w)
- B ∈ PreFirst(w) if Bv ∈ PreFirst(w)
- v ∈ PreFirst(w) if Bv ∈ PreFirst(w) and B erasable
- v ∈ PreFirst(w) for every A ∈ PreFirst(w) and rule A → v

Then First(w) consists of

- all terminal letters a ∈ T such that a ∈ PreFirst(w), and
- λ if w = A 1 A 2... An for n ≥ 0 and erasable variables A 1,..., An. (This is equivalent to w ⇒∗ λ.)

Definition. We consider the terminal letters that can follow a variable:

Follow(A) = { a ∈ T | S ⇒∗... Aa... }



Construction. We use $ as a special ‘ end of word’ symbol.

- Follow(S) ⊇ { $ }
- Follow(A) ⊇ First(w) \\ { λ } for every rule B → vAw
- Follow(A) ⊇ Follow(B) for rules B → vAw with λ ∈ First(w)

Definition (Parser table). The parser table for a context-free grammar is a table with

- columns indexed by terminals T ∪ {$},
- rows indexed by variables V,

At place \[a ∈ T ∪ {$}, B ∈ V \] it contains rules B → u for which

- a ∈ First(u), or (never the case for a = $)
- λ ∈ First(u) and a ∈ Follow(B).

Construction. LL parsing Given an LL(1)-grammar and parsing table. To parse a 1 · · · an, we start with ⟨S$, a 1 · · · an$⟩. From a state ⟨v, w⟩ we can do the following steps:

- ⟨av′, aw′⟩ becomes ⟨v′, w′⟩
- ⟨Bv′, aw′⟩ becomes ⟨uv′, aw′⟩ if B → u at position \[a, B\]
- ⟨Bv′, $⟩ becomes ⟨v′, $⟩ if B → u at position \[$, B\]
- ⟨$, $⟩ results in accept
- In all other cases, ⟨v, w⟩ results in reject!

#### 2 Nondeterministic Pushdown Automata

Definition (Pushdown automaton). A nondeterministic pushdown automaton ( NPDA) is a tuple (Q, Σ, Γ, δ, q 0, z, F ) consisting of a finite set of states Q, a finite input alphabet Σ, a finite stack alphabet Γ, a transition function δ: Q × (Σ ∪ { λ }) × Γ → 2 Q×Γ

∗ where δ(q, α, b) is always finite, a starting state q 0 ∈ Q, a stack starting symbol z ∈ Γ, and a set of final states F ⊆ Q.

Definition. The language generated by NPDA M = (Q, Σ, Γ, δ, q 0, z, F ) is

L(M ) = { w ∈ Σ∗ | (q 0, w, z) ⊢∗ (q′, λ, u) where q′ ∈ F }.

Remark (Acceptance with Empty Stack). In some literature, NPDAs are de- fined to accept with an empty stack (instead of final states). Then (empty stack) language of NPDA M is

Lλ(M ) = { w ∈ Σ∗ | (q 0, w, z) ⊢∗ (q′, λ, λ) }.




---

## 3. Recursively Enumerable Languages


### 3.1 Turing Machines


**Definition:** A deterministic Turing machine (TM) is a 7-tuple $(Q, \Sigma, \Gamma, \delta, q_0, 2, F)$ where:
- $Q$ is a finite set of states
- $\Sigma \subseteq \Gamma \setminus \{2\}$ is a finite input alphabet
- $\Gamma$ is a finite tape alphabet
- $\delta: Q \times \Gamma \to Q \times \Gamma \times \{L, R\}$ is a partial transition function
- $q_0$ is the starting state
- $2 \in \Gamma$ is the blank symbol
- $F \subseteq Q$ is the set of final (accepting) states

Assume $\delta(q, a)$ is undefined for every $q \in F$ and $a \in \Gamma$.

The language $L(M)$ accepted by TM $M$ is:
$$L(M) = \{ w \in \Sigma^* \mid q_0 w \vdash^* u q v \text{ for some } q \in F, u, v \in \Gamma^* \}$$

#### 3 Unrestricted Grammars

Construction (From Turing machines to grammars). Let M = (Q, Σ, Γ, δ, q 0, 2, F ) be a Turing machine. We construct an unrestricted grammar as follows. The variables are S, T, 2 and V γα, V qγα for every α ∈ Σ ∪ { 2 }, γ ∈ Γ and q ∈ Q.

Step 1: guessing the word w

S → V 22 S | SV 22 | T T → T V aa | V qa 0 a for every a ∈ Σ After step 1, we have derived something of the form

V 22 · · · V 22 V qa 01 a 1 V aa 22 V aa 33 · · · V aann V 22 · · · V 22

where w = a 1 a 2 · · · an. Step 2: simulating the TM (in the subscripts)

V qcαV γβ → V dα V qβ′ γ if δ(q, c) = (q′, d, R) V γβ V qcα → V qβ′ γ V dα if δ(q, c) = (q′, d, L)

for every α, β ∈ Σ ∪ { 2 } and γ ∈ Γ.

Step 3: If TM reaches accepting state, then generate w: V qγα → α for every q ∈ F βV γα → βα V γα β → αβ 2 → λ for every α, β ∈ Σ ∪ { 2 } and γ ∈ Γ.

Then L(G) = L(M ).

## Automata & Complexity Cheat Sheet 2022Automata & Complexity Cheat Sheet 2022


### 3.2 Post's Correspondence Problem

Theorem. The modified Posts Correspondence Problem (PCP) is undecidable.

Construction. Let G = (V, T, S, P ) be an unrestricted grammar. We can re- duce the question w ∈ L(G) to the modified PCP as follows. We define (where F and E are fresh):

w 1 = F v 1 = F S ⇒ w 2 = ⇒ wE v 2 = E... x


#### ...

. y (x → y ∈ P ) a a (a ∈ T ) A A (A ∈ V ) ⇒ ⇒

This MPCP has a solution ⇐⇒ w ∈ L(G).


---

## 4. Context-Sensitive Languages

Definition. A linear bounded automaton, short LBA, is a nondeterministic TM (Q, Σ, Γ, δ, q 0, F ) without 2, but with special symbols \[ and \], where

- \[ and \] are placed around the input word
- for every q ∈ Q, δ(q, \[ ) is of the form (q′, \[, R)
- for every q ∈ Q, δ(q, \] ) is of the form (q′, \], L)

Thus the head can only move within the bounds of the input word!

Definition. The language L(M ) accepted by LBA M = (Q, Σ, Γ, δ, q 0, F ) is

{ w ∈ Σ+ | q 0 \[w\] ⊢+ \[uqv\] for some q ∈ F, u, v ∈ Γ∗ }


---

## 5. Time and Space Complexity

#### 5 Bounded Tiling Problem
![[image-7.png]]
Theorem. The bounded tiling problem is NP-complete.

Construction (From Turing machines to the bounded tiling problem). Let M be a nondeterministic polynomial-time Turing machine. Then M has running time p(k) for some polynomial p(k). We give a polynomial-time reduction of ‘x ∈ L(M )?’ to the bounded tiling problem. For input word x = a 1 · · · ak we choose n = 2p(k) + 1. (Here we assume p(k) ≥ k, otherwise make it so.) As first row we choose:

![[image-8.png]]
![[image-9.png]]
![[image-10.png]]

Then, for input $x=a1· · · a(k)$ and with the indicated starting row:

$n×n$ field can be tiled   $⇐⇒$   x∈L(M)
Every tiling simulates a computation of Mon input x. The tiling can be finished
if and only if Mhas an accepting computation for input x.