Bayesian Approach
===

Consider two events $$A$$ and $$B$$. Based on the definition of the conditional probability we can follow:

$$\mathbb{P}[A\mid B]=\frac{\mathbb{P}[A\cap B]}{\mathbb{P}[B]}=\frac{\mathbb{P}[A\cap B]\,\mathbb{P}[A]}{\mathbb{P}[A]\, P[B]}=\frac{\mathbb{P}[B\mid A]\,\mathbb{P}[A]}{\mathbb{P}[B]}.$$
 
Let us call $$A$$ "the sought quantity $$X$$" and $$B$$ "the observation $$O$$". Bayes' theorem then has the form:

$$\mathbb{P}(X\mid O)=\mathbb{P}(X)\frac{\mathbb{P}(O\mid X)}{\mathbb{P}(O)}$$
 
This expression is meant to aid in the estimation of a model $$M$$ from observed data $$O$$. The ingredients of Bayes' theorem are called as follows:

|Symbol|Meaning|
|-----------------------|-------------------------|
| $$ \mathbb{P}(X\mid O) $$ |  posterior probability  |
| $$ \mathbb{P}(X) $$   |  prior probability of the sought quantity $$ X $$ |
| $$ \mathbb{P}(O) $$   |  prior probability of the data $$ O $$|
| $$ \mathbb{P}(O\mid X) $$ |  likelihood  |

In many cases we only work with one given dataset. Then, $$ \mathbb{P}(O)$$ is constant, and we find that the posterior probability, up to a normalization constant, is given by:

$$\mathbb{P}(X\mid O)\propto\mathbb{P}(X)\:\mathbb{P}(O\mid X)$$

Bayes' theorem is useful for estimation because often the quantities on the right hand side are known or easy to obtain. The likelihood $$\mathbb{P}(O\mid X)$$ is usually easy to evaluate for a given data set $$O$$ once we have specified the probability model with parameters $$X$$ produce the data. The prior $$\mathbb{P}(X)$$ is a probability that has the function to bias the estimator towards values of $$X$$ that are reasonable. If no prior is used that is equivalent to using a uniform prior, which may not always be a good choice. Choosing $$\mathbb{P}(X)$$ is a modeling problem, so there is "right" or "wrong" here and it must be chosen with expertise for the process observed. The significance of the prior is to be able to have a well-defined probability distribution even in the case that no or almost no data is at hand. When more and more data is collected, the likelihood $$\mathbb{P}(O\mid X)$$ will get sharper and thus eventually dominate the prior. Thus, it is generally a good idea to use a rather weak prior that rules out unphysical results but can be easily overcome when some data is collected.

When seeking optimial models we will maximize the posterior:

$$\mathbb{P}(X\mid O)\rightarrow{\rm max}$$
 
or alternatively we can draw samples $$x_{k}$$ from it, e.g. with a MCMC approach (see below):

$$x_{k}\sim\mathbb{P}(X\mid O)$$
 