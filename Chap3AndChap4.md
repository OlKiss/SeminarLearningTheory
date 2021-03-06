---
title: "Chap. 3&4"
---

# A Formal Learning Model and Learning via Uniform Convergence

### PAC(Probably Approximately correct) learning

A hypothesis class $\mathcal{H}$ is PAC learnable
if there exist a function $m_H : (0; 1)^2 \to \mathcal{N}$ and a learning algorithm with the
following property: For every $\delta, \epsilon \in (0; 1)$, for every distribution $\mathcal{D}$ over $\mathcal{X}$, and
for every labeling function $f : X \to {0; 1}$, if the realizable assumption holds
with respect to $\mathcal{H};\mathcal{D};f$, then when running the learning algorithm on $m \geq 
m_H(\delta; \epsilon)$ i.i.d. examples generated by $\mathcal{D}$ and labeled by $\mathcal{f}$, the algorithm returns
a hypothesis h such that, with probability of at least $1- \delta$ (over the choice of the examples),$ \mathcal{L}_{\mathcal{D},f}(h) \leq \epsilon$

$\epsilon$ - accuracy parameter (how far the output classifier from the optimal) - **Approximately**

$\delta$ - confidence parameter (how likely the classifier is to meet the accuracy requirement) - **Probably**

$m_H : (0; 1)^2 \to \mathcal{N}$ defines sample complexity (how many samples are needed)

### Corollary
Every finite hypothesis class is PAC learnable with following sample complexity:

$m_H(\delta; \epsilon) \leq \frac{\log\frac{\|\mathcal{H}\|}{\delta}}{\epsilon}$


### More general learning rile:

* Realizability assumption does not hold quite often

* Labels may not be fully determined by the features which we measure

$\Rightarrow \mathcal{D}$ should be considered as a probability distribution over $\mathcal{X}\times\mathcal{Y}$.
In other words, $\mathcal{D}$ - joint distribution over domain points and labels.

Let us redefine $\mathcal{L}_{\mathcal{D}}(h)$:

$\mathcal{L}\_{\mathcal{D}}(h) = \mathcal{P}\_{(x,y)\sim D}[h(x)\neq y] = \mathcal{D}(\{(x,y): h(x) \neq y\})$

And now we want learning algorithm to find a predictor whose error is not much larger than the best possible error of 
a predictor in some hypothesis class, given for bench marking.

#### Agnostic PAC
A hypothesis class $\mathcal{H}$ is agnostic PAC learnable
if there exist a function $m_H : (0; 1)^2 \to \mathcal{N}$ and a learning algorithm with the
following property: For every $\delta, \epsilon \in (0; 1)$, for every distribution $\mathcal{D}$ over $\mathcal{X}\times\mathcal{Y}$, when running learning algorithm on $m \geq 
m_H(\delta; \epsilon)$ i.i.d. examples generated by $\mathcal{D}$, the algorithm returns
a hypothesis $h$ such that, with probability of at least $1- \delta$ (over the choice of the examples),$ \mathcal{L}\_{\mathcal{D}}(h) \leq min_{h \in \mathcal{H}} \mathcal{L}_{\mathcal{D}}(h') + \epsilon$

In case of agnostic PAC, if realisability holds Agnostic PAC gives same guarantee as PAC, when realisability does not hold no learner can guarantee an arbitrarily small error, but it is still OK, since learner can still declare a success if its error
is not much larger than the best error achievable by a predictor from the class $\mathcal{H}$.

### Uniform convergence

A training set $\mathcal{S}$ is called $\epsilon$-representative
(w.r.t. domain $\mathcal{Z}$, hypothesis class $\mathcal{H}$, loss function $l$, and distribution $\mathcal{D}$) if 
$\forall h \in \mathcal{H}, \| \mathcal{L}\_{\mathcal{S}}(h) -  \mathcal{L}\_{\mathcal{D}}(h)\| \leq \epsilon$

Assume that a training set S is $\frac{\epsilon}{2}$-representative (w.r.t. domain $\mathcal{Z}$, hypothesis class $\mathcal{H}$, loss function $l$, and distribution $\mathcal{D}$). Then, any output of
$ERM_H(S)$, namely, any $h_S$ $\in$ $argmin_{h \in \mathcal{H}}$ $\mathcal{L}\_{S}(h)$, satisfies
$\mathcal{L}\_{\mathcal{D}}(h_S) \leq min\_{h \in \mathcal{H}}\mathcal{L}\_{\mathcal{D}}(h) + \epsilon$

##### Sketch of proof:

$\mathcal{L}\_{\mathcal{D}}(h_s) \leq \mathcal{L}\_{\mathcal{S}}(h_s) + \frac{\epsilon}{2} \leq \mathcal{L}\_{\mathcal{S}}(h) + \frac{\epsilon}{2} \leq \mathcal{L}\_{\mathcal{D}}(h) + \epsilon$


#### Uniform convergence:
We say that a hypothesis class $\mathcal{H}$ has
the uniform convergence property (w.r.t. a domain $\mathcal{Z}$ and a loss function l) if
there exists a function $m^\mathcal{UC}\_{\mathcal{H}} : (0; 1)^2 \to \mathcal{N}$ such that for every $\epsilon, \delta \in (0; 1)$ and for every probability distribution $\mathcal{D}$ over $\mathcal{Z}$, if $\mathcal{S}$ is a sample of $m \geq m^\mathcal{UC}_{\mathcal{H}}(\epsilon, \delta)$
examples drawn i.i.d. according to $\mathcal{D}$, then, with probability of at least $1 - \delta$, $\mathcal{S}$ is $\epsilon$-representative.

###### Finite classes are agnostic PAC learnable

$\mathcal{D}^m(\{\mathcal{S} : \forall h \in \mathcal{H} \| \mathcal{L}\_s(h) - \mathcal{L}\_\mathcal{D}(h)\| \leq \epsilon \}) \geq 1 - \delta$

Equals to

$\mathcal{D}^m(\{\mathcal{S} : \forall h \in \mathcal{H} \| \mathcal{L}\_s(h) - \mathcal{L}\_\mathcal{D}(h)\| > \epsilon \}) < 1 - \delta$

$\bigcup_{h \in \mathcal{H}}\{\mathcal{S}: \| \mathcal{L}\_s(h) - \mathcal{L}\_\mathcal{D}(h)\| > \epsilon \} \leq $

$\leq  \sum\_{h \in \mathcal{H}} \mathcal{D}^m(\{\mathcal{S} :\| \mathcal{L}\_s(h) - \mathcal{L}\_\mathcal{D}(h)\| > \epsilon\})$

At the same time:

$\mathcal{L}\_\mathcal{D}(h) = E[l(h,z)]$ and
$\mathcal{L}\_\mathcal{S}(h)=\frac{1}{m}\sum_{i=1}^{m}l(h,z_i)$ and
$\mathcal{L}\_\mathcal{S}(h) = \mathcal{L}\_\mathcal{D}(h)$

And using Hoeffding's Inequality:
$\mathcal{D}^m(\{\mathcal{S} : \forall h \in \mathcal{H} \| \mathcal{L}\_s(h) - \mathcal{L}\_\mathcal{D}(h)\| > \epsilon \}) < 1 - \delta$
$\leq \sum_{h \in H}2exp(-2m\epsilon^2) = 2|\mathcal{H}|exp(-2m\epsilon^2)$

#### Corollary

Let $\mathcal{H}$ be a finite hypothesis class, let $\mathcal{Z}$ be a domain and let $l: \mathcal{H} \times \mathcal{Z} \to{[0,1]}$ be a loss function, then $\mathcal{H}$ enjoys the uniform convergence with sample complexity:
$m_h^{uc}(\epsilon, \delta) \leq \frac{log(\frac{2|H|}{\delta})}{2\epsilon^2}$

### Questions:
1. How to approach a good hypothesis class?

2. P49 of the book, Remark 3.2, first sentence, why the algorithm will return a hypothesis from H?

3. P58,Exercise 1

4. P57，Remark 4.1("Discretization trick"). Is it really a trick to solve problem or something we have to deal with?

5.The bound of PAC learnability and bound of agnostic PAC learnability is different, why? and which part of the assumption makes the difference?






