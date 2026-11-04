# Lecture: Propositional and First-Order Logic

### Lecture Agenda
1. [**Introduction & The Big Ideas**](#1-introduction--the-big-ideas): Role of logic in AI, knowledge-based agents, and KR formalisms.
2. [**Propositional Logic (PL)**](#2-propositional-logic-pl): Syntax, connectives, truth tables, model checking, entailment, and limitations.
3. [**First-Order Logic (FOL) Foundations**](#3-first-order-logic-fol): Ontological commitments (objects, relations, functions), terms, and BNF grammar.
4. [**Quantifiers & Scoping**](#4-quantifiers): Universal ($\forall$) and existential ($\exists$) quantification, scope, order sensitivity, and De Morgan's laws.
5. [**Quantified Inference Rules**](#5-quantified-inference-rules): Universal/Existential Instantiation (Skolemization) and Generalization.
6. [**Translating Natural Language to FOL**](#6-translating-natural-language-english-to-first-order-logic): Translating complex English sentences and expressing exact numerical cardinality.
7. [**Genealogy Knowledge Base Case Study**](#7-case-study-genealogy-knowledge-base-in-fol): Axiomatic family tree relations, recursion, and query evaluation under CWA.
8. [**Comparison: PL vs. FOL**](#8-propositional-logic-vs-first-order-logic): Systematic comparison of expressiveness, complexity, and decidability.
9. [**Key Takeaways**](#9-key-takeaways): Summary of fundamental principles and practical AI trade-offs.
10. [**Exam Practice & Mastery Drills (Exam Replica & Full-Mark Guide)**](#10-exam-practice--mastery-drills): Scanned exam questions with complete solutions, pattern analysis, and replica practice sets with answer keys.

---

---

## 1. Introduction & The Big Ideas

Logic provides a formal, mathematically rigorous foundation for **Knowledge Representation (KR)** and **Reasoning** in Artificial Intelligence.

```
+-------------------------------------------------------------------------+
|                        KNOWLEDGE-BASED AGENT                            |
|                                                                         |
|    Sensors ---> [ Inference Engine ] <---> [ Knowledge Base (KB) ]     |
|                        |                  (Sentences in Logic)          |
|                        v                                                |
|   Actuators <-- [ Selected Action ]                                     |
+-------------------------------------------------------------------------+
```

### Core Insights
* **Logic as KR Language:** Expresses knowledge declaratively, allowing general-purpose inference algorithms to derive new facts.
* **Propositional Logic (PL):** A simple, boolean-based foundation with decidable inference, but limited in expressive power.
* **First-Order Logic (FOL):** Models the world in terms of objects, relations, and functions with quantifiers; significantly more expressive and widely used in AI.
* **Logic Variations:** Horn logic, Description Logics (e.g., OWL), Higher-Order Logic, Multi-Valued Logic, and Probabilistic Logics.

## 2. Propositional Logic (PL)

### 2.1 Syntax

Propositional logic represents facts as atomic boolean propositions combined using truth-functional connectives.

#### Primitive Components:
* **Logical Constants:** $\text{True}$ ($\top$), $\text{False}$ ($\bot$).
* **Propositional Symbols:** $P, Q, R, \dots$ representing atomic sentences (assertions about the world).
* **Parentheses:** $( \dots )$ specifying precedence and grouping.
* **Literal:** An atomic proposition ($P$) or its negation ($\neg P$).

#### Logical Connectives:

| Connective | Name | Alternate Symbols | Meaning |
| :---: | :--- | :---: | :--- |
| $\neg$ | Negation | $\sim$, $\text{NOT}$ | "NOT $P$" |
| $\wedge$ | Conjunction | $\&$, $\text{AND}$ | "$P$ AND $Q$" |
| $\vee$ | Disjunction | $\mid$, $\text{OR}$ | "$P$ OR $Q$" (inclusive) |
| $\to$ | Implication | $\implies$, $\supset$ | "If $P$, then $Q$" (Conditional) |
| $\leftrightarrow$ | Biconditional | $\equiv$, $\iff$ | "$P$ if and only if $Q$" (Equivalence) |

#### Well-Formed Formulas (WFF):
1. Any propositional symbol is a sentence.
2. If $S$ is a sentence, then $\neg S$ and $(S)$ are sentences.
3. If $S$ and $T$ are sentences, then $(S \wedge T)$, $(S \vee T)$, $(S \to T)$, and $(S \leftrightarrow T)$ are sentences.
4. Nothing else is a sentence.

---

### 2.2 Semantics & Truth Tables

The **semantics** of a sentence defines its truth value with respect to a particular **interpretation** (or assignment of truth values to each propositional symbol).

#### Standard Truth Table for Connectives:

| $P$ | $Q$ | $\neg P$ | $P \wedge Q$ | $P \vee Q$ | $P \to Q$ | $P \leftrightarrow Q$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ |
| $\text{F}$ | $\text{T}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ | $\text{F}$ |
| $\text{T}$ | $\text{F}$ | $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | $\text{F}$ |
| $\text{T}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ | $\text{T}$ | $\text{T}$ |

#### Deep Dive: The Implication Connective ($P \to Q$)
* In material implication, $P \to Q$ is **False only when the premise $P$ is True and conclusion $Q$ is False**.
* If $P$ is False, the implication $P \to Q$ is **vacuously True**, regardless of $Q$.
* When is $P \to Q$ True?
  - [x] $P = \text{True}, Q = \text{True}$
  - [x] $P = \text{False}, Q = \text{False}$
  - [x] $P = \text{False}, Q = \text{True}$
  - [ ] $P = \text{True}, Q = \text{False}$ (Only case where it is False)

---

### 2.3 Models and Entailment

* **Model:** A formal mathematical world—specifically, a complete truth assignment to all propositional symbols that makes a sentence (or Knowledge Base) **True**.
* **Knowledge Base ($KB$):** A set of sentences representing what the agent knows.
* **$M(KB)$:** The set of all models of the knowledge base.

#### Model Checking Example:
Consider a Knowledge Base with symbols:
* $P$: "It is hot"
* $Q$: "It is humid"
* $R$: "It is raining"

$$KB_1 = \{ (P \wedge Q) \to R, \; Q \to P \}$$

Let's test all $2^3 = 8$ truth assignments:

| $P$ | $Q$ | $R$ | $P \wedge Q$ | $(P \wedge Q) \to R$ | $Q \to P$ | $KB_1$ Model? |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $\text{F}$ | $\text{F}$ | $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ | **OK** |
| $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ | **OK** |
| $\text{F}$ | $\text{T}$ | $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | No |
| $\text{F}$ | $\text{T}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | No |
| $\text{T}$ | $\text{F}$ | $\text{F}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ | **OK** |
| $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{T}$ | **OK** |
| $\text{T}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | $\text{F}$ | $\text{T}$ | No |
| $\text{T}$ | $\text{T}$ | $\text{T}$ | $\text{T}$ | $\text{T}$ | $\text{T}$ | **OK** |

> [!NOTE]
> If we now observe that **$Q$ is True** and add it to the knowledge base:
> $$KB_2 = \{ (P \wedge Q) \to R, \; Q \to P, \; Q \}$$
> The only model that satisfies all three sentences simultaneously is **$\text{TTT}$** ($P = \text{True}, Q = \text{True}, R = \text{True}$).

---

### 2.4 Logical Properties & Definitions

* **Tautology (Valid Sentence):** A sentence that evaluates to $\text{True}$ under **all possible interpretations**.
  $$\text{Example: } P \vee \neg P \quad \text{("It is raining or it is not raining")}$$
* **Contradiction (Inconsistent / Unsatisfiable):** A sentence that evaluates to $\text{False}$ under **all possible interpretations**.
  $$\text{Example: } P \wedge \neg P \quad \text{("It is raining and it is not raining")}$$
* **Satisfiable:** A sentence is satisfiable if it is True in at least one interpretation.
* **Entailment ($\alpha \models \beta$):** $\alpha$ entails $\beta$ if and only if in every model in which $\alpha$ is True, $\beta$ is also True:
  $$M(\alpha) \subseteq M(\beta)$$
* **Modus Ponens Inference Rule:**
  $$\frac{\alpha \to \beta, \quad \alpha}{\beta}$$

---

### 2.5 Strengths and Limitations of Propositional Logic

#### Advantages:
* Simple syntax and unambiguous semantics.
* Foundation for higher-order logics.
* **Decidable:** Algorithmic verification always terminates in finite time.
* Highly optimized SAT solvers (DPLL, WalkSAT) efficiently solve instances with millions of variables.

#### Disadvantages:
* **Extremely low expressiveness:** Cannot directly quantify over objects or relationships.
* **Combinatorial Explosion:** Requires duplicating rules for every individual object.
  * To say *"Every block on the table is green"*, propositional logic requires:
    $$(\text{Block1OnTable} \to \text{Block1Green}) \wedge (\text{Block2OnTable} \to \text{Block2Green}) \wedge \dots$$
* Lacks mechanisms to express generalizations or handle infinite domains.

---

## 3. First-Order Logic (FOL)

First-Order Logic (also known as **First-Order Predicate Calculus**) solves the limitations of propositional logic by adopting an ontological commitment to a world consisting of **objects**, **properties**, **relations**, and **functions**.

```mermaid
flowchart TD
    FOL[World in First-Order Logic]
    FOL --> Objects["Objects: Things with individual identities\n(Aly, Book, Car, 5)"]
    FOL --> Properties["Properties: Distinguish individual objects\n(Red, Large, Prime, Student)"]
    FOL --> Relations["Relations: Connections among sets of objects\n(BrotherOf, BiggerThan, Owns)"]
    FOL --> Functions["Functions: Total mappings with a unique output\n(FatherOf, BestFriendOf, Sqrt)"]
```

---

### 3.1 Elements and User-Provided Symbols

| Component | Definition | Examples |
| :--- | :--- | :--- |
| **Constants** | Name specific individual objects in the domain | $\text{Aly}, \text{Ahmed}, \text{BlueBox}, 5$ |
| **Variables** | Stand for unspecified objects in the domain | $x, y, z, \text{foo}$ |
| **Functions** | Map tuples of objects to another unique object | $\text{father\_of}(\text{Aly}) = \text{Ahmed}$, $\text{color\_of}(\text{Sky}) = \text{Blue}$ |
| **Predicates** | Map tuples of objects to a truth value ($\text{True}/\text{False}$) | $\text{greater}(5, 3)$, $\text{green}(\text{Grass})$, $\text{color}(\text{Grass}, \text{Green})$ |
| **Connectives** | Connect sentences identical to PL | $\neg, \wedge, \vee, \to, \leftrightarrow$ |
| **Quantifiers** | State assertions over collections of objects | Universal ($\forall$), Existential ($\exists$) |

---

### 3.2 Terms and Sentences

* **Term:** A logical expression denoting a real-world object.
  * Base terms: A constant symbol or a variable symbol.
  * Complex terms: An $n$-place function applied to $n$ terms: $f(t_1, t_2, \dots, t_n)$.
  * **Ground Term:** A term containing **no variables** (e.g., $\text{John}$, $\text{father\_of}(\text{father\_of}(\text{John}))$).
* **Atomic Sentence:** The most basic formula that carries a truth value ($\text{True}$ or $\text{False}$).
  * Formed by an $n$-place predicate applied to $n$ terms:
    $$P(t_1, t_2, \dots, t_n)$$
  * Or an equality between two terms:
    $$t_1 = t_2$$
  * *Examples:* $\text{green}(\text{Kermit})$, $\text{brother}(\text{Aly}, \text{Omar})$, $\text{eats}(\text{Ahmed}, \text{GoudaCheese})$.
* **Complex Sentence:** Sentences combined using logical connectives:
  $$\neg P, \quad P \wedge Q, \quad P \vee Q, \quad P \to Q, \quad P \leftrightarrow Q$$
* **Well-Formed Formula (WFF):** A quantified sentence where all variables are **bound** by an enclosing quantifier.
  * *Example:* $\forall x \, P(x, y)$ has $x$ bound, but $y$ is free (not a closed sentence/wff).

---

### 3.3 Backus-Naur Form (BNF) Grammar for FOL

```bnf
<Sentence>        ::= <AtomicSentence>
                    | "(" <Sentence> ")"
                    | "NOT" <Sentence>
                    | <Sentence> <Connective> <Sentence>
                    | <Quantifier> <Variable>, ... <Sentence>

<AtomicSentence>  ::= <Predicate> "(" <Term>, ... ")"
                    | <Term> "=" <Term>

<Term>            ::= <Function> "(" <Term>, ... ")"
                    | <Constant>
                    | <Variable>

<Connective>      ::= "AND" | "OR" | "IMPLIES" | "EQUIVALENT"

<Quantifier>      ::= "FORALL" | "EXISTS"

<Constant>        ::= "Aly" | "Ahmed" | "John" | "A" | "5" | ...
<Variable>        ::= "x" | "y" | "z" | "s" | ...
<Predicate>       ::= "Student" | "Smart" | "Bigger" | "Color" | ...
<Function>        ::= "FatherOf" | "MotherOf" | "LeftLegOf" | ...
```

---

## 4. Quantifiers

Quantifiers allow expressing statements about collections of objects without enumerating them individually.

### 4.1 Universal Quantification ($\forall$)
* **Syntax:** $\forall x \, P(x)$
* **Meaning:** $P$ holds for **all** values of $x$ in the domain of discourse.
* **Standard Idiom with Implication ($\to$):**
  $$\forall x \, (\text{student}(x) \to \text{smart}(x)) \quad \equiv \quad \text{"All students are smart"}$$

> [!WARNING] Common Mistake with $\forall$:
> Writing $\forall x \, (\text{student}(x) \wedge \text{smart}(x))$ means:  
> *"Everyone in the entire universe is a student and is smart!"*  
> Universal quantifiers are **almost always used with implication ($\to$)**, not conjunction ($\wedge$).

---

### 4.2 Existential Quantification ($\exists$)
* **Syntax:** $\exists x \, P(x)$
* **Meaning:** $P$ holds for **at least one** value of $x$ in the domain.
* **Standard Idiom with Conjunction ($\wedge$):**
  $$\exists x \, (\text{student}(x) \wedge \text{smart}(x)) \quad \equiv \quad \text{"There exists a student who is smart"}$$

> [!WARNING] Common Mistake with $\exists$:
> Writing $\exists x \, (\text{student}(x) \to \text{smart}(x))$ is vacuously true if there is *anyone in the universe who is NOT a student* (since $\text{False} \to \text{Anything}$ is $\text{True}$).  
> Existential quantifiers are **almost always used with conjunction ($\wedge$)**, not implication ($\to$).

---

### 4.3 Quantifier Scope & Ordering

The order of quantifiers is critical when mixing $\forall$ and $\exists$.

```
           +---------------------------------------+
           | (∀x) alive(x)  ->  (∃y) loves(x, y)   |
           +---------------------------------------+
             |                    |
             | Scope of x         | Scope of y
             +--------------------+
```

#### Commutativity Rules:
1. **Identical quantifiers commute:**
   $$\forall x \forall y \, P(x, y) \equiv \forall y \forall x \, P(x, y) \quad \text{("All dogs hate all cats")}$$
   $$\exists x \exists y \, P(x, y) \equiv \exists y \exists x \, P(x, y) \quad \text{("A cat killed a dog")}$$
2. **Mixed quantifiers DO NOT commute:**
   $$\forall x \exists y \, \text{likes}(x, y) \quad \neq \quad \exists y \forall x \, \text{likes}(x, y)$$
   * $\forall x \exists y \, \text{likes}(x, y)$: *"Everyone likes someone"* (each person may like a different person).
   * $\exists y \forall x \, \text{likes}(x, y)$: *"There is someone whom everyone likes"* (one universal popular person).

---

### 4.4 Duality & De Morgan's Laws for Quantifiers

The universal and existential quantifiers are duals of each other across negation:

| De Morgan Law | Natural Language Example |
| :--- | :--- |
| $\forall x \, \neg P(x) \iff \neg \exists x \, P(x)$ | *"All dogs do not like cats"* $\equiv$ *"No dogs like cats"* |
| $\neg \forall x \, P(x) \iff \exists x \, \neg P(x)$ | *"Not all dogs dance"* $\equiv$ *"There is a dog that does not dance"* |
| $\forall x \, P(x) \iff \neg \exists x \, \neg P(x)$ | *"All dogs sleep"* $\equiv$ *"There is no dog that does not sleep"* |
| $\exists x \, P(x) \iff \neg \forall x \, \neg P(x)$ | *"There is a dog that talks"* $\equiv$ *"Not all dogs can't talk"* |

---

## 5. Quantified Inference Rules

Classical propositional inference rules (e.g., Modus Ponens, Resolution) are generalized to First-Order Logic via four quantifier manipulation rules:

```mermaid
graph LR
    subgraph Elimination
        UI["Universal Instantiation\n(∀-Elimination)"]
        EI["Existential Instantiation\n(∃-Elimination / Skolemization)"]
    end
    subgraph Introduction
        UG["Universal Generalization\n(∀-Introduction)"]
        EG["Existential Generalization\n(∃-Introduction)"]
    end
```

### 1. Universal Instantiation (Universal Elimination)
From a universally quantified sentence, infer any ground instance by substituting a ground term $c$ for variable $x$:
$$\frac{\forall x \, P(x)}{P(c)}$$

* *Example:*
  $$\forall x \, \text{eats}(\text{Ahmed}, x) \implies \text{eats}(\text{Ahmed}, \text{GoudaCheese})$$
  $$\forall x \, \text{eats}(\text{Ahmed}, x) \implies \text{eats}(\text{Ahmed}, \text{contents}(\text{BlueBox}))$$

---

### 2. Existential Instantiation (Existential Elimination / Skolemization)
From an existentially quantified sentence, infer that $P$ holds for a **brand-new Skolem constant** $k$ that has never appeared anywhere in the Knowledge Base:
$$\frac{\exists x \, P(x)}{P(k)}$$

* *Example:*
  $$\exists x \, \text{eats}(\text{Aly}, x) \implies \text{eats}(\text{Aly}, K_1)$$
* **Condition:** $K_1$ must be a freshly minted symbol (Skolem constant) representing that unknown individual, preventing invalid inferences.

---

### 3. Existential Generalization (Existential Introduction)
If a sentence holds for a specific constant $c$, we can infer that an existential statement holds:
$$\frac{P(c)}{\exists x \, P(x)}$$

* *Example:*
  $$\text{eats}(\text{Ahmed}, \text{GoudaCheese}) \implies \exists x \, \text{eats}(\text{Ahmed}, x)$$
* **Constraint:** Variable $x$ must not already occur free in the original formula.

---

### 4. Universal Generalization (Universal Introduction)
If an expression $P(c)$ has been proven for an arbitrary constant $c$ about which no prior assumptions have been made, infer $\forall x \, P(x)$:
$$\frac{P(c) \quad \text{for an arbitrary } c}{\forall x \, P(x)}$$

---

## 6. Translating Natural Language (English) to First-Order Logic

Converting English statements into First-Order Logic requires identifying the domain objects, appropriate predicates, functions, and proper quantifier scope.

### Translation Catalog

| English Statement | First-Order Logic Representation |
| :--- | :--- |
| **"Every gardener likes the sun."** | $\forall x \, (\text{gardener}(x) \to \text{likes}(x, \text{Sun}))$ |
| **"You can fool some of the people all of the time."** | $\exists x \, \forall t \, (\text{person}(x) \wedge (\text{time}(t) \to \text{can\_fool}(x, t)))$ |
| **"You can fool all of the people some of the time."** | $\forall x \, \exists t \, (\text{person}(x) \to (\text{time}(t) \wedge \text{can\_fool}(x, t)))$ |
| **"All purple mushrooms are poisonous."** | $\forall x \, ((\text{mushroom}(x) \wedge \text{purple}(x)) \to \text{poisonous}(x))$ |
| **"No purple mushroom is poisonous."** *(Method 1: $\neg \exists$)* | $\neg \exists x \, (\text{mushroom}(x) \wedge \text{purple}(x) \wedge \text{poisonous}(x))$ |
| **"No purple mushroom is poisonous."** *(Method 2: $\forall$)* | $\forall x \, ((\text{mushroom}(x) \wedge \text{purple}(x)) \to \neg \text{poisonous}(x))$ |
| **"Abdallah is not short."** | $\neg \text{short}(\text{Abdallah})$ |

---

### Advanced Translation: Exact Cardinality
*"There are exactly two purple mushrooms."*

To express exact quantities in FOL without numerical primitives, we state:
1. There exist two objects $x$ and $y$ that are purple mushrooms.
2. $x$ and $y$ are distinct ($x \neq y$).
3. Any object $z$ that is a purple mushroom must be identical to either $x$ or $y$.

$$\begin{aligned}
\exists x \, \exists y \, \Big[ & \text{mushroom}(x) \wedge \text{purple}(x) \wedge \text{mushroom}(y) \wedge \text{purple}(y) \wedge \neg(x = y) \\
& \wedge \forall z \, \big( (\text{mushroom}(z) \wedge \text{purple}(z)) \to (z = x \vee z = y) \big) \Big]
\end{aligned}$$

---

## 7. Case Study: Genealogy Knowledge Base in FOL

Building an axiomatic Knowledge Base allows an automated theorem prover to infer relationships not explicitly stated.

### 7.1 Predicates
* $\text{male}(x)$, $\text{female}(x)$
* $\text{parent}(x, y)$, $\text{child}(x, y)$
* $\text{father}(x, y)$, $\text{mother}(x, y)$, $\text{son}(x, y)$, $\text{daughter}(x, y)$
* $\text{spouse}(x, y)$, $\text{husband}(x, y)$, $\text{wife}(x, y)$
* $\text{ancestor}(x, y)$, $\text{descendant}(x, y)$, $\text{relative}(x, y)$

### 7.2 Ground Facts
```prolog
husband(Mohamed, Radwa)
son(Aly, Tamer)
spouse(Ahmed, Laila)
male(Ahmed)
son(Omar, Laila)
father(Mahmoud, Laila)
daughter(Farida, Mahmoud)
daughter(Amal, Farida)
```

### 7.3 Axiomatic Definitional Rules

#### Parent / Child Relationships:
$$\forall x, y \, (\text{parent}(x, y) \leftrightarrow \text{child}(y, x))$$
$$\forall x, y \, (\text{father}(x, y) \leftrightarrow (\text{parent}(x, y) \wedge \text{male}(x)))$$
$$\forall x, y \, (\text{mother}(x, y) \leftrightarrow (\text{parent}(x, y) \wedge \text{female}(x)))$$
$$\forall x, y \, (\text{daughter}(x, y) \leftrightarrow (\text{child}(x, y) \wedge \text{female}(x)))$$
$$\forall x, y \, (\text{son}(x, y) \leftrightarrow (\text{child}(x, y) \wedge \text{male}(x)))$$

#### Spouse & Marriage:
$$\forall x, y \, (\text{spouse}(x, y) \leftrightarrow \text{spouse}(y, x)) \quad \text{; Symmetric relation}$$
$$\forall x, y \, (\text{husband}(x, y) \leftrightarrow (\text{spouse}(x, y) \wedge \text{male}(x)))$$
$$\forall x, y \, (\text{wife}(x, y) \leftrightarrow (\text{spouse}(x, y) \wedge \text{female}(x)))$$

#### Ancestor & Descendant (Recursive Transitive Closure):
$$\forall x, y \, (\text{parent}(x, y) \to \text{ancestor}(x, y)) \quad \text{; Base case}$$
$$\forall x, y, z \, ((\text{parent}(x, z) \wedge \text{ancestor}(z, y)) \to \text{ancestor}(x, y)) \quad \text{; Recursive step}$$
$$\forall x, y \, (\text{descendant}(x, y) \leftrightarrow \text{ancestor}(y, x))$$

#### Kinship / Relative Rules:
$$\forall x, y, z \, ((\text{ancestor}(z, x) \wedge \text{ancestor}(z, y)) \to \text{relative}(x, y)) \quad \text{; Common ancestor}$$
$$\forall x, y \, (\text{spouse}(x, y) \to \text{relative}(x, y)) \quad \text{; Related by marriage}$$
$$\forall x, y, z \, ((\text{relative}(z, x) \wedge \text{relative}(z, y)) \to \text{relative}(x, y)) \quad \text{; Transitivity}$$
$$\forall x, y \, (\text{relative}(x, y) \leftrightarrow \text{relative}(y, x)) \quad \text{; Symmetry}$$

### 7.4 Sample Queries & Inference

| Query Sentence | Expected Result | Explanation |
| :--- | :---: | :--- |
| $\text{ancestor}(\text{Mahmoud}, \text{Aly})$ | **Yes** | Derived via parent/child relations chain |
| $\text{relative}(\text{Amal}, \text{Tamer})$ | **Yes** | Shares common lineage via ancestry axioms |
| $\text{relative}(\text{Laila}, \text{Abdallah})$ | **No** (under CWA) | Cannot be proven; assumed false under Closed World Assumption |
| $\exists z \, (\text{ancestor}(z, \text{Fred}) \wedge \text{ancestor}(z, \text{Liz}))$ | **Variable Binding** | Asks: *"Do Fred and Liz share an ancestor?"* |

---

## 8. Propositional Logic vs. First-Order Logic

| Feature | Propositional Logic (PL) | First-Order Logic (FOL) |
| :--- | :--- | :--- |
| **Ontological Commitments** | Facts (propositions) that hold or do not hold | Objects, Properties, Relations, and Functions |
| **Epistemological Commitments** | True, False, or Unknown | True, False, or Unknown |
| **Expressive Power** | Low (rigid boolean propositions) | High (quantifiers, predicates, relations) |
| **Sentence Conciseness** | Verbose / un-concise for large domains | Compact, elegant parameterized expressions |
| **Inference Decidability** | **Decidable** (NP-Complete / co-NP-Complete) | **Semi-Decidable** (entailment is recursively enumerable) |
| **Algorithmic Solvers** | SAT Solvers (DPLL, CDCL, WalkSAT) | Resolution refutation, unification, theorem provers |
| **Common AI Uses** | Circuit verification, planning, constraint satisfaction | Knowledge graphs, semantic web (OWL), natural language semantics |

---

## 9. Key Takeaways

1. **Formal KR:** Logic allows an AI agent to represent beliefs explicitly and deduce new knowledge soundly.
2. **PL as Foundation:** Propositional logic is simple and decidable, but lacks expressiveness because it cannot reference objects or general rules.
3. **FOL Primitives:** FOL models the world using **Objects**, **Properties**, **Relations**, and **Functions**.
4. **Quantifier Idioms:**
   * Universal quantification ($\forall$) naturally pairs with implication ($\to$).
   * Existential quantification ($\exists$) naturally pairs with conjunction ($\wedge$).
5. **Order Matters:** While $\forall x \forall y$ and $\exists x \exists y$ are commutative, switching $\forall x \exists y$ and $\exists y \forall x$ drastically alters semantic meaning.
6. **Inference Bridge:** Quantifier instantiation rules (Universal Elimination and Skolemization) connect First-Order sentences to propositional theorem proving engines.
7. **Computational Trade-off:** FOL gains enormous expressiveness at the expense of semi-decidability (proving non-entailment may not terminate on infinite domains).

---

## 10. Exam Practice & Mastery Drills

This section provides a rigorous, step-by-step methodology to solve any First-Order Logic translation question, highlights the exact traps examiners use to deduct marks, deconstructs the **actual exam questions** from your test paper, and provides matched practice sets with full model answers.

---

### 10.1 Step-by-Step Solver Guide: How to Tackle Translation Questions

#### Part A: English $\to$ FOL Translation (The 5-Step Pipeline)

```mermaid
flowchart TD
    S1["Step 1: Identify Quantifiers & Scope\n(All/Every -> ∀, There is/Some -> ∃)"]
    S2["Step 2: Classify Entities\n(Constants = Bill/AI, Predicates = Student/Smart)"]
    S3["Step 3: Select the Canonical Connective\n(∀ pairs with ->, ∃ pairs with ∧)"]
    S4["Step 4: Check Constraints & Modifiers\n('Other' -> ¬(x=y), 'Either/or' -> XOR, Cardinality)"]
    S5["Step 5: Sanity Check & Boundary Testing\n(Check variable binding & vacuous truth)"]
    S1 --> S2 --> S3 --> S4 --> S5
```

##### Step 1: Detect Quantifiers from Keyword Triggers
* **Universal Triggers ($\forall$):** *"Every"*, *"All"*, *"Each"*, *"Any"*, *"Whoever"*, *"Whatever"*.
* **Existential Triggers ($\exists$):** *"There exists"*, *"There is"*, *"Some"*, *"At least one"*, *"A/An"* (when referring to existence, e.g., *"a student passed"*).
* **Negative Triggers ($\neg\exists$ or $\forall \neg$):** *"No"*, *"None"*, *"Nobody"*, *"Nothing"*, *"Never"*.

##### Step 2: Separate Objects (Constants) from Categories (Predicates)
* **Constants (Named Individuals):** Specific people, courses, semesters, or places are constants, passed as arguments inside predicates:
  * $\text{Bill}$, $\text{AI}$, $\text{History}$, $\text{Spring2024}$.
  * > [!CAUTION] Do **not** create predicates out of proper constants! Writing $\text{AI}(x)$ or $\text{Bill}(x)$ is invalid syntax and loses marks. Bill is an entity $\text{Bill}$; AI is a course object $\text{AI}$.
* **Unary Predicates (Types & Properties):** General categories and single properties:
  * $\text{Student}(x)$, $\text{Smart}(x)$, $\text{Course}(c)$.
* **$N$-ary Predicates (Relations & Actions):** Connections between two or more objects:
  * $\text{Passed}(x, c)$, $\text{Loves}(x, y)$, $\text{Attended}(x, c, s)$.

##### Step 3: Apply the Canonical Connective Rule (The Golden Law of Logic)
| Quantifier | Required Primary Connective | General Schema | Why? |
| :---: | :---: | :---: | :--- |
| **Universal ($\forall$)** | **Conditional ($\to$)** | $\forall x \, (\text{Condition}(x) \to \text{Property}(x))$ | If an object does not meet the condition, the implication is vacuously true, preserving the domain constraint. |
| **Existential ($\exists$)** | **Conjunction ($\wedge$)** | $\exists x \, (\text{Condition}(x) \wedge \text{Property}(x))$ | You are asserting that an entity simultaneously exists in the category **and** exhibits the property. |

##### Step 4: Handle Special Modifiers & Relational Nuances
* **"Some other / another":** When an entity acts on another entity of the same kind, enforce distinctness with $\neg(x = y)$:
  $$\forall x \, (\text{Student}(x) \to \exists y \, (\text{Student}(y) \wedge \neg(x = y) \wedge \dots))$$
* **"Either $A$ or $B$ (but not both)":** This is exclusive OR ($\text{XOR}$). Standard FOL lacks an official $\oplus$ connective, so expand it explicitly:
  $$(A \vee B) \wedge \neg(A \wedge B) \quad \text{or} \quad (A \wedge \neg B) \vee (\neg A \wedge B)$$
* **"Only":** "Only students study" means if someone studies, they are a student ($\text{Studies}(x) \to \text{Student}(x)$). "Only $A$ are $B$" $\equiv \forall x (B(x) \to A(x))$.

##### Step 5: Perform the "Vacuous Truth" Boundary Test
Ask yourself: *What happens if the universe has no students (or no one who took AI)?*
* If you wrote $\forall x (\text{Student}(x) \wedge \text{Smart}(x))$: if a cat exists in the universe, the sentence evaluates to **False** (a fatal flaw).
* If you wrote $\exists x (\text{Student}(x) \to \text{Smart}(x))$: if a cat exists (not a student), $\text{False} \to \text{Smart}(\text{cat})$ is **True**, making your sentence automatically True even if not a single student exists!

---

#### Part B: FOL $\to$ English Translation (Inside-Out Decoding)

Translating from logic back into English requires identifying recognized semantic patterns rather than rendering clumsy mechanical word-by-word text:

```
+-------------------------------------------------------------------------------------------------------+
| FOL FORMULA FINGERPRINT                                  | NATURAL ENGLISH TRANSLATION               |
+-------------------------------------------------------------------------------------------------------+
| ¬∃x (Student(x) ∧ P(x))                                  | "No student is P."                         |
| ∀x (Student(x) -> ¬P(x))                                 | "No student is P." (Equivalent to above)   |
+-------------------------------------------------------------------------------------------------------+
| ∃x (P(x) ∧ ∀y (P(y) => x = y))                           | "Exactly one object is P."                 |
| ∃x (Student(x) ∧ Failed(x, H) ∧ ∀y (... => x = y))      | "Exactly one student failed H."            |
+-------------------------------------------------------------------------------------------------------+
| ∃x ∃y (P(x) ∧ P(y) ∧ ¬(x = y))                           | "There are at least two distinct P's."    |
| ∃x ∃y (SisterOf(x, B) ∧ SisterOf(y, B) ∧ ¬(x = y))       | "Bill has at least two sisters."           |
+-------------------------------------------------------------------------------------------------------+
| ∀x ∀y ((P(x) ∧ P(y)) -> x = y)                           | "There is at most one P."                  |
+-------------------------------------------------------------------------------------------------------+
| ¬∃x (P(x) ∧ ∀y (P(y) ∧ ¬(x=y) => R(x,y)))               | "No P does R to every other P."            |
+-------------------------------------------------------------------------------------------------------+
```

##### 3-Step Translation Technique:
1. **Identify the Core Predicates:** List the nouns and verbs involved (e.g., $x$ is a student, $x$ failed History).
2. **Decode the Structural Frame:** Look for cardinality idioms (e.g., uniqueness $\forall y (\dots \implies x = y)$, multiplicity $\neg(x = y)$, or total negation $\neg\exists$).
3. **Draft Both Literal and Idiomatic Sentences:** Write the literal meaning first to verify logical fidelity, then write the clean, idiomatic English sentence on your exam sheet.

---

### 10.2 Fatal Exam Mistakes & Best Practices to Avoid Them

The following table summarizes the most frequent deduction causes observed on introductory AI exams:

| Error Category | Common Student Mistake | Why Marks Are Deducted | Correct Full-Credit Version |
| :--- | :--- | :--- | :--- |
| **1. The $\forall$-with-$\wedge$ Disaster** | $\forall x \, (\text{Student}(x) \wedge \text{Smart}(x))$ | Asserts that every single entity in existence is a student and is smart. | $\forall x \, (\text{Student}(x) \to \text{Smart}(x))$ |
| **2. The $\exists$-with-$\to$ Disaster** | $\exists x \, (\text{Student}(x) \to \text{Passed}(x))$ | Vacuously satisfied by any non-student object in the universe (a rock, a dog). | $\exists x \, (\text{Student}(x) \wedge \text{Passed}(x))$ |
| **3. Forgetting Distinctness ($\neg(x = y)$)** | $\forall x \, (\text{Student}(x) \to \exists y \, (\text{Student}(y) \wedge \text{Loves}(x, y)))$ | Fails to enforce *"some other"*; allows $x = y$ (students loving themselves). | Add $\neg(x = y)$ inside the existential scope. |
| **4. Mistaking "At least 2" for "Two"** | Translating $\exists x \exists y (\dots \wedge \neg(x=y))$ as *"There are two sisters."* | $\exists x \exists y$ does not forbid a third sister; it means **at least two**. | Write: *"Bill has at least two sisters."* |
| **5. Missing Uniqueness Condition** | Translating $\exists x (\text{Student}(x) \wedge \text{Failed}(x) \wedge \dots)$ as *"A student failed."* | Ignores the universal clause $\forall y (\dots \implies x=y)$ which enforces uniqueness. | Write: *"Exactly one student failed."* |
| **6. Making Constants into Predicates** | $\forall x \, (\text{AI}(x) \to \dots)$ or $\text{Bill}(x)$ | $\text{Bill}$ and $\text{AI}$ are specific ground terms (objects), not unary classes. | Use predicates over terms: $\text{Studied}(x, \text{AI})$ |
| **7. Free / Unbound Variables** | $\forall x \, (\text{Student}(x) \to \text{Loves}(x, y))$ | $y$ is free (unquantified), making the sentence an invalid WFF. | Ensure every variable has an enclosing $\forall$ or $\exists$. |

---

### 10.3 Scanned Exam Paper: Complete Solutions & Scoring Breakdown

Here is the exact solution sheet for the test paper shown in the exam scan:

```
+----------------------------------------------------------------------------------------------------+
|                                    ACTUAL EXAM PAPER DECONSTRUCTION                                 |
+----------------------------------------------------------------------------------------------------+
```

#### Question (Two): Translate English Statements into FOL [5 Degrees]

##### Statement A: *"All students who studied AI are smart."*
* **Analysis:** Universal statement over students with a composite condition (being a student **and** having studied AI).
* **Predicate Definitions:**
  * $\text{Student}(x)$: "$x$ is a student"
  * $\text{Studied}(x, \text{AI})$: "$x$ studied AI"
  * $\text{Smart}(x)$: "$x$ is smart"
* **FOL Formula:**
  $$\forall x \, ((\text{Student}(x) \wedge \text{Studied}(x, \text{AI})) \to \text{Smart}(x))$$
* **Grading Trap:** Never use $\wedge$ as the main connective with $\forall$:
  * *Incorrect:* $\forall x \, (\text{Student}(x) \wedge \text{Studied}(x, \text{AI}) \wedge \text{Smart}(x))$ (Means every entity in the universe is a student, studied AI, and is smart).

---

##### Statement B: *"There is a student who passed AI in Spring 2024."*
* **Analysis:** Existential statement asserting the simultaneous existence of an entity who is a student and passed AI during a specific semester.
* **Predicate Definitions:**
  * $\text{Student}(x)$: "$x$ is a student"
  * $\text{Passed}(x, c, s)$: "$x$ passed course $c$ in semester $s$" (or ternary predicate $\text{Passed}(x, \text{AI}, \text{Spring2024})$)
* **FOL Formula:**
  $$\exists x \, (\text{Student}(x) \wedge \text{Passed}(x, \text{AI}, \text{Spring2024}))$$
  *(Acceptable alternative if using separate predicates:)*
  $$\exists x \, (\text{Student}(x) \wedge \text{Passed}(x, \text{AI}) \wedge \text{TakenIn}(x, \text{Spring2024}))$$
* **Grading Trap:** Never use $\to$ with $\exists$. $\exists x \, (\text{Student}(x) \to \dots)$ is vacuously true if anything in the universe is not a student.

---

##### Statement C: *"There is a smart student who attended courses in Spring 2024."*
* **Analysis:** Existential statement over a student who satisfies two properties: being smart, and having attended at least one course in Spring 2024.
* **Predicate Definitions:**
  * $\text{Student}(x)$, $\text{Smart}(x)$
  * $\text{Course}(c)$: "$c$ is a course"
  * $\text{Attended}(x, c, s)$: "$x$ attended course $c$ in semester $s$"
* **FOL Formula (Most Rigorous / Preferred):**
  $$\exists x \, (\text{Student}(x) \wedge \text{Smart}(x) \wedge \exists c \, (\text{Course}(c) \wedge \text{Attended}(x, c, \text{Spring2024})))$$
* **Acceptable Compact Form (If course is treated relationally):**
  $$\exists x \, (\text{Student}(x) \wedge \text{Smart}(x) \wedge \text{AttendedCourses}(x, \text{Spring2024}))$$

---

##### Statement D: *"Bill takes either Analysis or Geometry (but not both)."*
* **Analysis:** Exclusive OR ($\text{XOR}$ / $\oplus$). True if Bill takes Analysis and not Geometry, OR Bill takes Geometry and not Analysis.
* **Predicate Definition:** $\text{Takes}(p, c)$: "$p$ takes course $c$"
* **FOL Formula (Standard Definition of XOR):**
  $$(\text{Takes}(\text{Bill}, \text{Analysis}) \vee \text{Takes}(\text{Bill}, \text{Geometry})) \wedge \neg(\text{Takes}(\text{Bill}, \text{Analysis}) \wedge \text{Takes}(\text{Bill}, \text{Geometry}))$$
* **Alternative Equivalent Form:**
  $$(\text{Takes}(\text{Bill}, \text{Analysis}) \wedge \neg\text{Takes}(\text{Bill}, \text{Geometry})) \vee (\neg\text{Takes}(\text{Bill}, \text{Analysis}) \wedge \text{Takes}(\text{Bill}, \text{Geometry}))$$
* **Biconditional Negation Form:**
  $$\text{Takes}(\text{Bill}, \text{Analysis}) \leftrightarrow \neg\text{Takes}(\text{Bill}, \text{Geometry})$$

---

##### Statement E: *"Every student loves some other student."*
* **Analysis:** Universal quantifier on students, existential on another student. The keyword **"other"** demands that the two students are distinct ($x \neq y$).
* **FOL Formula:**
  $$\forall x \, (\text{Student}(x) \to \exists y \, (\text{Student}(y) \wedge \neg(x = y) \wedge \text{Loves}(x, y)))$$
* **Grading Trap:** Forgetting $\neg(x = y)$ loses half the mark. Without $\neg(x = y)$, a student could love themselves, violating *"some other student"*.

---

#### Question (Three): Translate FOL into English Statements [5 Degrees]

##### Formula A:
$$\neg\exists x \, (\text{Student}(x) \wedge \text{Loves}(x, \text{Bill}))$$
* **Literal Reading:** "It is not thecase that there exists an $x$ such that $x$ is a student and $x$ loves Bill."
* **Natural English (Full-Mark Answer):**
  > **"No student loves Bill."** *(or "There is no student who loves Bill.")*
* **Equivalent Form:** $\forall x \, (\text{Student}(x) \to \neg\text{Loves}(x, \text{Bill}))$ ("All students do not love Bill").

---

##### Formula B:
$$\exists x \, (\text{Student}(x) \wedge \text{Failed}(x, \text{History}) \wedge \forall y \, (\text{Student}(y) \wedge \text{Failed}(y, \text{History}) \implies x = y))$$
* **Pattern Recognition:** This is the classical FOL idiom for **Uniqueness / Exact Cardinality of 1**.
  * $\exists x \, (\dots)$: There exists a student $x$ who failed History.
  * $\forall y \, (\dots \implies x = y)$: Any student $y$ who failed History must be that exact same person $x$.
* **Natural English (Full-Mark Answer):**
  > **"Exactly one student failed History."** *(or "Only one student failed History.")*
* > [!WARNING] Don't just write "There is a student who failed History". You must capture the uniqueness constraint $\forall y (\dots \implies x=y)$.

---

##### Formula C:
$$\neg\exists x \, (\text{Student}(x) \wedge \text{Failed}(x, \text{Chemistry})) \wedge \exists x \, (\text{Student}(x) \wedge \text{Failed}(x, \text{History}))$$
* **Breakdown:** Conjunction of two independent quantified clauses:
  1. $\neg\exists x \, (\text{Student}(x) \wedge \text{Failed}(x, \text{Chemistry}))$: "No student failed Chemistry."
  2. $\exists x \, (\text{Student}(x) \wedge \text{Failed}(x, \text{History}))$: "At least one student failed History."
* **Natural English (Full-Mark Answer):**
  > **"No student failed Chemistry, and (at least) one student failed History."**
  *(or: "While no student failed Chemistry, some student failed History.")*

---

##### Formula D:
$$\exists x \exists y \, (\text{SisterOf}(x, \text{Bill}) \wedge \text{SisterOf}(y, \text{Bill}) \wedge \neg(x = y))$$
* **Pattern Recognition:** Two existential variables with an explicit inequality $\neg(x = y)$ represents **"at least two"**.
* **Literal Reading:** "There exist two individuals $x$ and $y$ such that $x$ is a sister of Bill, $y$ is a sister of Bill, and $x$ is not equal to $y$."
* **Natural English (Full-Mark Answer):**
  > **"Bill has at least two sisters."** *(or "There are at least two different sisters of Bill.")*

---

##### Formula E:
$$\neg\exists x \, (\text{Student}(x) \wedge \forall y \, (\text{Student}(y) \wedge \neg(x = y) \implies \text{Fools}(x, y)))$$
* **Breakdown from Inside Out:**
  * $\text{Student}(y) \wedge \neg(x = y)$: "any other student $y$".
  * $\forall y \, (\text{Student}(y) \wedge \neg(x = y) \implies \text{Fools}(x, y))$: "$x$ fools every other student".
  * $\text{Student}(x) \wedge \dots$: "a student $x$ who fools every other student".
  * $\neg\exists x \, (\dots)$: "there does not exist such a student".
* **Natural English (Full-Mark Answer):**
  > **"No student fools every other student."** *(or "There is no student who fools all other students.")*

---

### 10.4 The 6 Architectural Patterns Tested in University Exams

Every translation question on midterm and final AI exams tests one of six canonical forms:

```
+-------------------------------------------------------------------------------------------------------+
| Pattern 1: Universal Conditional Assertion                                                            |
| English: "All X with property P do Y"                                                                 |
| FOL:     ∀x ((X(x) ∧ P(x)) -> Y(x))                                                                   |
+-------------------------------------------------------------------------------------------------------+
| Pattern 2: Existential Instance with Context                                                          |
| English: "There is an X who did Y in context C"                                                       |
| FOL:     ∃x (X(x) ∧ Y(x, C))                                                                          |
+-------------------------------------------------------------------------------------------------------+
| Pattern 3: Exclusive Choice (Either / Or but not both)                                                |
| English: "A does P or Q but not both"                                                                 |
| FOL:     (P(A) ∨ Q(A)) ∧ ¬(P(A) ∧ Q(A))                                                               |
+-------------------------------------------------------------------------------------------------------+
| Pattern 4: Relational Action on a Distinct Object                                                     |
| English: "Every X does R to some other X"                                                             |
| FOL:     ∀x (X(x) -> ∃y (X(y) ∧ ¬(x = y) ∧ R(x, y)))                                                  |
+-------------------------------------------------------------------------------------------------------+
| Pattern 5: Exact Numerical Cardinality (At least, At most, Exactly)                                    |
| • At least two: ∃x ∃y (P(x) ∧ P(y) ∧ ¬(x = y))                                                        |
| • At most one:  ∀x ∀y ((P(x) ∧ P(y)) -> x = y)                                                        |
| • Exactly one:  ∃x (P(x) ∧ ∀y (P(y) -> x = y))                                                        |
+-------------------------------------------------------------------------------------------------------+
| Pattern 6: Universal/Existential Negation                                                             |
| English: "No X does Y"                                                                                |
| FOL:     ¬∃x (X(x) ∧ Y(x))   [Identical to: ∀x (X(x) -> ¬Y(x))]                                       |
+-------------------------------------------------------------------------------------------------------+
```

---

### 10.5 Exam-Replica Practice Set 1: English $\to$ FOL

> **Instructions:** Translate each of the following 5 statements into First-Order Logic formulas. Use clear predicate names. (5 Points)

1. **Question 1A:** All professors who teach Machine Learning are knowledgeable.
2. **Question 1B:** There is a doctor who treated COVID patients in Winter 2021.
3. **Question 1C:** There is a talented musician who performed concerts in Paris in 2023.
4. **Question 1D:** Omar passed either Linear Algebra or Calculus (but not both).
5. **Question 1E:** Every researcher collaborates with some other researcher.

<details>
<summary><b>Click to View Model Answers & Explanations (Set 1)</b></summary>

* **1A:**
  $$\forall x \, ((\text{Professor}(x) \wedge \text{Teaches}(x, \text{MachineLearning})) \to \text{Knowledgeable}(x))$$
* **1B:**
  $$\exists x \, (\text{Doctor}(x) \wedge \text{Treated}(x, \text{COVID}, \text{Winter2021}))$$
  *(or: $\exists x \, (\text{Doctor}(x) \wedge \exists p \, (\text{Patient}(p) \wedge \text{Has}(p, \text{COVID}) \wedge \text{Treated}(x, p, \text{Winter2021})))$)*
* **1C:**
  $$\exists x \, (\text{Musician}(x) \wedge \text{Talented}(x) \wedge \exists c \, (\text{Concert}(c) \wedge \text{PerformedIn}(x, c, \text{Paris}, 2023)))$$
* **1D:**
  $$(\text{Passed}(\text{Omar}, \text{LinearAlgebra}) \vee \text{Passed}(\text{Omar}, \text{Calculus})) \wedge \neg(\text{Passed}(\text{Omar}, \text{LinearAlgebra}) \wedge \text{Passed}(\text{Omar}, \text{Calculus}))$$
* **1E:**
  $$\forall x \, (\text{Researcher}(x) \to \exists y \, (\text{Researcher}(y) \wedge \neg(x = y) \wedge \text{CollaboratesWith}(x, y)))$$

</details>

---

### 10.6 Exam-Replica Practice Set 2: FOL $\to$ English

> **Instructions:** Translate each of the following FOL formulas into clear, natural English statements. (5 Points)

1. **Question 2A:**
   $$\neg\exists x \, (\text{Employee}(x) \wedge \text{Disrespects}(x, \text{Manager}))$$
2. **Question 2B:**
   $$\exists x \, (\text{Politician}(x) \wedge \text{ElectedPresident}(x) \wedge \forall y \, (\text{Politician}(y) \wedge \text{ElectedPresident}(y) \implies x = y))$$
3. **Question 2C:**
   $$\neg\exists x \, (\text{Runner}(x) \wedge \text{Injured}(x, \text{Marathon})) \wedge \exists x \, (\text{Runner}(x) \wedge \text{BrokeRecord}(x, \text{Marathon}))$$
4. **Question 2D:**
   $$\exists x \exists y \, (\text{BrotherOf}(x, \text{Sarah}) \wedge \text{BrotherOf}(y, \text{Sarah}) \wedge \neg(x = y))$$
5. **Question 2E:**
   $$\neg\exists x \, (\text{Player}(x) \wedge \forall y \, (\text{Player}(y) \wedge \neg(x = y) \implies \text{Defeats}(x, y)))$$

<details>
<summary><b>Click to View Model Answers & Explanations (Set 2)</b></summary>

* **2A:** **"No employee disrespects the manager."** *(or "There is no employee who disrespects the manager.")*
* **2B:** **"Exactly one politician was elected president."** *(or "Only one politician was elected president.")*
* **2C:** **"No runner was injured in the marathon, and at least one runner broke a record in the marathon."**
* **2D:** **"Sarah has at least two brothers."**
* **2E:** **"No player defeats every other player."** *(or "There is no player who beats all other players.")*

</details>

---

### 10.7 High-Yield Advanced Exam Variations (To Guarantee 100%)

Examiners love introducing slight twists to the core templates. Master these 5 variations:

#### Variation 1: "At most one student scored 100 in AI."
* **Formula:**
  $$\forall x \forall y \, ((\text{Student}(x) \wedge \text{Scored100}(x, \text{AI}) \wedge \text{Student}(y) \wedge \text{Scored100}(y, \text{AI})) \to x = y)$$
* *Logic:* If any two students scored 100, they must actually be the same person. (Allows 0 or 1, but never 2).

#### Variation 2: "There is a course that every student passed." vs "Every student passed some course."
* **There is a course that every student passed:**
  $$\exists c \, (\text{Course}(c) \wedge \forall s \, (\text{Student}(s) \to \text{Passed}(s, c)))$$
  *(One single shared course exists).*
* **Every student passed some course:**
  $$\forall s \, (\text{Student}(s) \to \exists c \, (\text{Course}(c) \wedge \text{Passed}(s, c)))$$
  *(Each student may have passed a completely different course).*

#### Variation 3: "No two distinct students share the same ID."
* **Formula:**
  $$\forall x \forall y \, ((\text{Student}(x) \wedge \text{Student}(y) \wedge \neg(x = y)) \to \neg(\text{ID}(x) = \text{ID}(y)))$$
  *(Or equivalently: $\forall x \forall y \, ((\text{Student}(x) \wedge \text{Student}(y) \wedge \text{ID}(x) = \text{ID}(y)) \to x = y)$)*

#### Variation 4: "Not all smart students take AI."
* **Formula (Direct):**
  $$\neg \forall x \, ((\text{Student}(x) \wedge \text{Smart}(x)) \to \text{Takes}(x, \text{AI}))$$
* **Formula (De Morgan Dual):**
  $$\exists x \, (\text{Student}(x) \wedge \text{Smart}(x) \wedge \neg\text{Takes}(x, \text{AI}))$$
  *Both are 100% equivalent and earn full credit.*

#### Variation 5: "Only students who study pass AI."
* **Key English Distinction:** "Only $P$ are $Q$" means $Q \to P$ (not $P \to Q$).
* **Formula:**
  $$\forall x \, ((\text{Student}(x) \wedge \text{Passes}(x, \text{AI})) \to \text{Studies}(x))$$

---

### 10.8 The Full-Mark Exam Day Checklist

Before handing in your exam paper, verify each sentence against this 5-point checklist:

- [ ] **Universal ($\forall$) uses $\to$:** Ensure your $\forall x$ statement does NOT have $\wedge$ as its primary connective.
- [ ] **Existential ($\exists$) uses $\wedge$:** Ensure your $\exists x$ statement does NOT have $\to$ as its connective.
- [ ] **"Other" or "Distinct" checks $\neg(x = y)$:** Whenever the English prompt mentions *"another"*, *"some other"*, *"two different"*, or *"someone else"*, check that $\neg(x = y)$ is explicitly included.
- [ ] **Exactness checks Uniqueness ($\forall y (\dots \implies x = y)$):** "Exactly one" requires BOTH the existential existence of $x$ AND the universal condition that forces all candidates to equal $x$.
- [ ] **All variables are bound:** Count every variable ($x, y, z$) inside predicates and ensure each one is governed by an enclosing $\forall$ or $\exists$. Free variables will immediately lose marks.


