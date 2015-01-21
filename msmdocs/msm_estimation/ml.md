Maximum likelihood or maximum probability estimators
===

An important class of estimators are those which estimate the likelihood $$ \mathbb{P}(O\mid X)$$  or the posterior probability $$\mathbb{P}(X\mid O)$$. There are a number of common principles and tricks that can be exploited to derive such estimators. Here, we will focus on maximum likelihood estimators, although most principles are applicable to estimators that maximize the posterior probability.


Neglect normalization constants
----

Often, likelihoods are of the form

$$\mathbb{P}(O\mid X)	=	Z^{-1}w(O\mid X)	\propto w(O\mid X)$$

where Z^{-1} is a normalization constant and w(O\mid X) is an unnormalized probability weight. The maximum is independent of the normalization constant:
 
\max_{X}\mathbb{P}(O\mid X)=\max_{X}w(O\mid X)
 
and therefore the normalization constant can be neglected in the process of seeking the maximum.

Convert likelihood to log-likelihood
---

Often likelihoods consist of products of statistically independent components, such as:\mathbb{P}(O\mid X)\propto\prod_{i}w(o_{i}\mid x_{i})
 This form is difficult to work with due to the product. For optimization purposes it is therefore a common “trick” to instead work with the logarithm of the likelihood (log-likelihood):Q=\log\mathbb{P}(O\mid X)=\sum_{i}\log w(o_{i}\mid x_{i}).
 This is useful since the logarithm is a monotonic function: as a result, the maximum of \log f
  is also the maximum of f
 . 

Incorporating constraints
---

In practice, one often needs to constraint the values of the parameters X
  in order to make sure that the estimate is structurally or physically meaningful. A common type of contraint is the equality constraint, such as \sum_{i}x_{i}=1
 . We add such constraints as Langrangian multiplyiers to Q
 , and obtain a Langrangian function such asL=Q+\lambda\left(1-\sum_{i}x_{i}\right)
 If there are no constraints, we simply have L=Q
 .

Solving
---

Now we seek the maximum of L
 . For this, we take the derivatives of the Langrangian and set them to zero. This yields the optimality conditions:\frac{\partial L}{\partial x_{i}}=0\:\:\:\:\forall i.
 If there are constraints, then we first need to solve for the Langrangian multipliers. This is usually done by solving the optimality conditions for x_{i}
 , inserting them into the constraint equations and then attempting to solve for \lambda
 .

Once we have solved for \lambda
 , we insert their value into the optimality conditions and obtain the maximum likelihood results for x_{i}
 .

In both, the solution for \lambda
  and the solution for x_{i}
 , it is possible that we cannot obtain a closed solution. In this case we have to approximate the solution numerically, e.g. by formulating a fixed-point iteration that will iteratively solve the constraint equations and/or optimality conditions, or by employing other approaches such as a Newton solver.

Example
---

Let us consider that we draw balls from an urn that contains black and white balls with an unknown fraction. We draw n_{w}
  white and n_{b}
  black balls. The likelihood of this outcome is proportional to\mathbb{P}(O\mid X)\propto p_{w}^{n_{w}}p_{b}^{n_{b}}
 The log-likelihood isQ=n_{w}\ln p_{w}+n_{b}\ln p_{b}
 We add the constraint p_{w}+p_{b}=1
  and obtain the Lagrangian:L=n_{w}\ln p_{w}+n_{b}\ln p_{b}+\lambda(1-p_{w}-p_{b})
 We take the derivatives and set them zero:\frac{\partial L}{\partial p_{w}}	=	\frac{n_{w}}{p_{w}}-\lambda=0
\frac{\partial L}{\partial p_{b}}	=	\frac{n_{b}}{p_{b}}-\lambda=0
 We insert these equations into the constraint equation p_{w}+p_{b}=1
  and rewrite them to:\frac{n_{w}}{\lambda}+\frac{n_{b}}{\lambda}	=	1
\lambda	=	n_{w}+n_{b}
 As a result, we get the maximum likelihood estimators:p_{w}	=	\frac{n_{w}}{n_{w}+n_{b}}
p_{b}	=	\frac{n_{b}}{n_{w}+n_{b}}
 Of course this result is obvious. However the procedure sketched above also works in much less obvious cases.