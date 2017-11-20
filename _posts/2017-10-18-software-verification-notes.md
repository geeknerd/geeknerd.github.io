---
layout: post
title: Notes on comprehending software verification.
excerpt: "Some not-that-well-structured notes during the study of software verification. Including pieces from various sources and mainly plays as a review and combination of the materials I went through."
date: 2017-11-20
modifited: 2017-11-20
comments: true
pinned: true
tags: [Notes, Software Engineering]
---

Software verification is a new area of study to me and I feel the realm of it could be deployed in a wide range of industries. Thus the overall learning process should be fun to me. 

<!--more-->

### Hoare logic[^1]
[^1]:<https://en.wikipedia.org/wiki/Hoare_logic>
**Predicate:**  
  Boolean-valued function $$P: X \to \{true, false\}$$ is called the predicate on X.  

**Imperative programming:**  
  programming paradigm that uses statements that change a program's state.  

**Hoare triple $$\{P\} C \{Q\}$$**  
  Whenever  P holds of the state before the execution of C, then Q will hold afterwards, or C does not terminate. $$\to$$ partial correctness only 

**Assignment rule:** $$ \{x+1 = 43\}\ y := x + 1\ \{ y = 43 \} $$ 

**Composition rule:**  
$$\{ x + 1 = 43 \}\ y := x + 1\ \{ y = 43 \}$$ 
and 
$$\{ y = 43 \}\ z := y\ \{ z = 43 \}$$

By the sequencing rule, one concludes: 
$$\{ x + 1 = 43 \}\ y := x + 1; z := y\ \{ z = 43 \}$$ 

**Conditional rule:** 
$$\{0 ≤ x ≤ 15 \}\ \text{if}\ x < 15\ \text{then}\ x := x + 1\ \text{else}\ x := 0\ \text{endif}\ \{0 ≤ x ≤ 15 \}$$

**Consequence rule:** 
Strengthen precondition / weaken postcondition  

**While rule:**  
\\[
\frac{ \\{P \land B \\}\ S\ \\{P\\}}{\\{P\\}\ \text{while}\ B\ \text{do}\ S\ \text{done}\ \\{ \neg B \land P\\}}
\\]
A proof of:  
$$\{x ≤ 10\}$$ while $$x < 10$$ do $$x := x + 1$$ done $$\{\neg x < 10 ∧ x \leq 10\}$$  
is reduced to proof of:  
$$\{x ≤ 10 ∧ x < 10\}\ x := x + 1\ \{x ≤ 10 \}$$,  
or simplified  
$$\{x < 10\}\ x := x + 1\ \{x ≤ 10\}$$. 

$$\{true\}$$ **while** $$x * x \neq a$$ **do skip done** $$\{x * x = a \land true\}$$  
$$\to$$ 
$$\{true \land x * x \neq a\}$$ **skip** $$\{true\}$$ (skip rule and consequence rule)

Because the program is either proved to be meet the post condition or it does not terminate, **while rule** only provides *partial correctness*. 

**While rule for total correctness**  
Introduces a *loop variant*, defined on a *well-founded ordering* < on some domain set D. 

### Predicate transformer semantics [^2]
[^2]:<https://en.wikipedia.org/wiki/Predicate_transformer_semantics>
Reducing the problem of verifying a Hoare triple to the problem of proving a first-order formula. 

Essentially, it's producing a precondition based on a statement and postcondition. 

A weaker precondition is better because it is less restrictive of the possible starting values of a program that ensure correctness. Typically, given a postcondition of a desired property of the output state, we would like to know the weakest precondition that guarantees the correctness. 

Given a program $$S$$ and a postcondition $$\varphi$$, the weakest property of the input state that guarantees that $$S$$ halts in a state satisfying $$\varphi$$ is called the *weakest precondition* of $$S$$ and $$\varphi$$ and is denoted $$wp(S,\varphi)$$. [^3]

[^3]:<http://www.cs.cornell.edu/courses/cs6110/2011sp/lectures/lecture18.pdf>

**Assignment:**  
$$
\begin{align}
wp(x:=x-5,x>10)& = x-5>10 \\
& \Leftrightarrow x>15
\end{align}
$$

**Sequence:**  
$$
\begin{align}
wp(x:=x-5;x:=x*2,x>20)
&= wp(x:x=5, wp(x:=x*2,x>20))\\
&= wp(x:=x-5,x*2>20)\\
&= (x-5)*2>20\\
&= x>15
\end{align}
$$