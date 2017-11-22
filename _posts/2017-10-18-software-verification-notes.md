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
  Whenever  P holds of the state before the execution of C, then Q will hold afterwards, or C does not terminate. $$\to$$ **partial correctness** only.

On the contrary, **total correctness** guarantees program's termination so C will terminate and Q will be the final state. 
{: .notice}

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
$$
\begin{align}
\frac{ \{P \land B \}\ S\ \{P \} }{\{P\}\ \text{while}\ B\ \text{do}\ S\ \text{done}\ \{ \neg B \land P \} }
\end{align}
$$

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
$$
\begin{align}
\frac{< \text{is a well-founded ordering on the set}\ D, [P \land B \land t \in D \land t=z]\quad S\quad [P \land t \in D \land t<z]}{[P\land t \in D]\ \mathbf{while}\ B\ \mathbf{do}\ S\ \mathbf{done}\ [\neg B \land P \land t \in D]}
\end{align}
$$

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

**Conditional:**  
$$
\begin{align}
wp(\mathbf{if}\ x<y\ \mathbf{then}\ x:=y\ \mathbf{else\ skip\ end}, x\geq y)
&= (x<y \Rightarrow wp(x:=y, x\geq y)) \land (\neg(x<y) \Rightarrow wp(\text{skip}, x\geq y))\\
&= (x<y \Rightarrow y\geq y) \land (\neg(x<y) \Rightarrow x\geq y)\\
& \Leftrightarrow \mathbf{true}
\end{align}
$$  

*Why the inference leads to a weakest precondition of **true**?*
{: .notice}

**While loop:**  

*Why necessary to use a loop invariant **I** since **I** stays true from the beginning to termination?*
{: .notice}