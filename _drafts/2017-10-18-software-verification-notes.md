---
layout: post
title: Notes on comprehending software verification.
excerpt: "Some not-that-well-structured notes during the study of software verification. Including pieces from various sources and mainly plays as a review and combination of the materials I went through."
date: 2017-10-18
comments: true
pinned: true
tags: [Notes]
---

Software verification is a new area of study to me and I feel the realm of it could be deployed in a wide range of industries. Thus the overall learning process should be fun to me. 

<!--more-->

### Hoare Logic
Predicate:  
  Boolean-valued function $$P: X \to \{true, false\}$$ is called the predicate on X.  

Imperative programming:  
  programming paradigm that uses statements that change a program's state.  

Hoare triple $$\{P\} C \{Q\}$$  
  Whenever  P holds of the state before the execution of C, then Q will hold afterwards, or C does not terminate. $$\to$$ partial correctness only 

Assignment rule: $$ \{x+1 = 43\}\ y := x + 1\ \{ y = 43 \} $$ 

Composition rule:  
$$\{ x + 1 = 43 \}\ y := x + 1\ \{ y = 43 \}$$ 
and 
$$\{ y = 43 \}\ z := y\ \{ z = 43 \}$$

By the sequencing rule, one concludes: 
$$\{ x + 1 = 43 \}\ y := x + 1; z := y\ \{ z = 43 \}$$ 

Conditional rule: 
$$\{0 ≤ x ≤ 15 \}\ \text{if}\ x < 15\ \text{then}\ x := x + 1\ \text{else}\ x := 0\ \text{endif}\ \{0 ≤ x ≤ 15 \}$$

Consequence rule: 
Strengthen precondition / weaken postcondition  

While rule:  
\\[
\frac{ \{P \land B \} S \{P\}}{\{P} \text{while} B \text{do} S \text{done} \{ \neg B \land P\}}
\\]
A proof of:  
$$\{x ≤ 10\}$$ while $$x < 10$$ do $$x := x + 1$$ done $$\{\neg x < 10 ∧ x \leq 10\}$$ 
is reduced to proof of : 
$$\{x ≤ 10 ∧ x < 10\}\ x := x + 1\ \{x ≤ 10 \}$$, or simplified  
$$\{x < 10\}\ x := x + 1\ \{x ≤ 10\}$$. 

$$\{true\}$$ **while** $$x * x \neq a$$ **do skip done** $$\{x * x = a \land true\}$$  
$$\to$$ 
$$\{true \land x * x \neq a\}$$ **skip** $$\{true\}$$, 