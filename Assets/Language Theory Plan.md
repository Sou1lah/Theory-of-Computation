## Week 1 - Foundations & Practice

### Day 1 - Introduction
- [ ] Learn: Formal languages, syntax vs semantics, models
- [ ] Practice: Define arithmetic language (`0,1,+,×,<`)
- [ ] Practice: Write 3 formulas and check manually if true in ℕ
- [ ] Mini-project: None

### Day 2 - Syntax vs Semantics
- [ ] Learn: Satisfaction \(M ⊨ φ\)
- [ ] Practice: Pick finite model `{0,1,2}`; write 2 formulas true, 2 false
- [ ] Mini-project: None

### Day 3 - Logical Connectives & Quantifiers
- [ ] Learn: ∧, ∨, ¬, →, ↔, ∀, ∃
- [ ] Practice: Translate “All students passed” and “Some numbers are even”
- [ ] Practice: Draw truth tables for formulas in a finite model

### Day 4 - Structures & Models
- [ ] Learn: Structures, substructures, extensions, isomorphisms
- [ ] Practice: Represent a small graph as a structure; write `∀x ∃y edge(x,y)`
- [ ] Mini-project: Optional start of Family Tree language

### Day 5 - Decision Problems & Satisfiability
- [ ] Learn: Satisfiable vs unsatisfiable formulas
- [ ] Practice: Pick 3 formulas; find a model satisfying each
- [ ] Mini-project: Begin Family Tree domain: define constants, predicates

### Day 6 - Mini-Project: Family Tree
- [ ] Define constants (`Alice`, `Bob`)
- [ ] Define predicates/functions (`Parent(x,y)`)
- [ ] Define constraints (no loops, max 2 parents)
- [ ] Check formulas manually
- [ ] Optional: Implement Family Tree model in Python

### Day 7 - Review & Practice
- [ ] Review: Syntax, semantics, quantifiers, models
- [ ] Practice: Write 5 formulas for a mini-system (traffic lights, library books)
- [ ] Optional: Read about first-order logic compactness

---

## Week 2 - Advanced Applications & Final Project

### Day 8 - Finite Models & Model Checking
- [ ] Learn: Finite models, domain restrictions, model checking basics
- [ ] Practice: Implement tiny Python model checker for finite sets
- [ ] Test formulas from Week 1 mini-projects

### Day 9 - Graphs & Relations
- [ ] Learn: Graphs as models, reachability, adjacency
- [ ] Practice: Represent small network; write formulas like “every node has a neighbor”
- [ ] Extend Python checker to graph models

### Day 10 - Logic in CS Systems
- [ ] Learn: Database queries as logic formulas, invariants
- [ ] Practice: Encode small DB (library/books) in logic
- [ ] Verify constraints: e.g., no book borrowed by multiple students

### Day 11 - Programming Integration
- [ ] Learn: Map formulas to Python structures (sets, dicts)
- [ ] Practice: Implement satisfaction checking
- [ ] Mini-project: Automate checking for Family Tree or DB models

### Day 12 - Complex Constraints & Planning Final Project
- [ ] Learn: Nested quantifiers, complex formulas
- [ ] Practice: Write 5+ complex formulas for final project
- [ ] Plan final project: domain, language, formulas, constraints

### Day 13 - Final Project: Implementation
- [ ] Build model system (e.g., University Course Enrollment)
- [ ] Implement Python-based model checker for your system

### Day 14 - Final Project: Testing & Presentation
- [ ] Test all constraints, debug formulas
- [ ] Visualize model (graph, tables)
- [ ] Document: language, models, formulas, results

---

## Resources

### YouTube :
- [William Fiset – Graph Theory and Relations](https://www.youtube.com/@WilliamFiset-videos)

### Articles / Tutorials
- [Stanford Encyclopedia of Philosophy – Model Theory](https://plato.stanford.edu/entries/model-theory/)
- [Wikipedia – Model Theory](https://en.wikipedia.org/wiki/Model_theory)

### Textbooks
- *A Mathematical Introduction to Logic* – Herbert Enderton
- *Logic in Computer Science: Modelling and Reasoning about Systems* – Michael Huth & Mark Ryan
- *Introduction to Model Theory* – Philipp Rothmaler

### Tools / Websites
- [Z3 SMT Solver](https://github.com/Z3Prover/z3)
- [Coq Proof Assistant](https://coq.inria.fr/)
- Python (sets & dicts) – for mini/final project implementation
