Linear Error Propagation
===

We consider $$n$$ random variables $$x_{1},...,x_{n}$$ that we aggregate in the vector $$\mathbf{x}=(x_{1},...,x_{m})^{T}$$. $$x_{j}$$ are distributed according to probability distribution $$p(x_{1},...,x_{n})=p(\mathbf{x})$$. We assume that we have the probability distribution $$p$$ available and can compute its maximum over $$\mathbf{x}$$ and the variances and covariances of the $$x$$-variables. However, we are interested in another set of random variables $$\mathbf{y}=(y_{1},...,y_{m})^{T}$$ that are given by a generally nonlinear function of $$x_{1},...,x_{n}$$:

$$ y_{1}	=	f_{1}(x_{1},...,x_{n})$$
$$ \vdots $$
$$ y_{m}	=	f_{n}(x_{1},...,x_{n})$$


Let us assume that the direct evaluation of the distribution $$p(\mathbf{y})$$ is difficult, such that we cannot easily calculate maxima and variances of the $$y$$-variables directly. In particular we are interested in “error propagation”, i.e. how the variances in $$\mathbf{x}$$ propagate through the $$f$$ onto $$\mathbf{y}$$. We are now seeking an approximate way to do this.

One approach is to estimate the uncertainties on $$y_{i}$$ by Monte Carlo sampling. Here, we investigate linear error propagation, which provides an analytical result, but at the sacrifice of making two approximations:

1. The distribution function of $$x_{i}$$ is approximated by a multivariate Gaussian, and
2. the functions $$f_{j}$$ are linearized.

Clearly, these approximations are only meaningful in certain situations, especially if the distribution is monomodal and near-Gaussian around its maximum, and if the $$f_{j}$$ are close-to linear within the high-probability range of $$x_{i}$$.

Gaussian approximation of the density
----

We first seek the $$\mathbf{x}$$ that maximizes the probability density $$p(\mathbf{x})$$:

$$ \hat{\mathbf{x}}=\arg\max p(\mathbf{x}) $$

By definition, the gradient at $$\hat{\mathbf{x}}$$ is zero. Next, we calculate second derivative matrix $$H$$, the Hessian matrix:

$$\Sigma^{-1}=H=\left[\begin{array}{ccc}
\frac{\partial p(\mathbf{x})}{\partial x_{1}x_{1}} & \cdots & \frac{\partial p(\mathbf{x})}{\partial x_{n}x_{1}}\\
\vdots &  & \vdots\\
\frac{\partial p(\mathbf{x})}{\partial x_{1}x_{n}} & \cdots & \frac{\partial p(\mathbf{x})}{\partial x_{n}x_{n}}
\end{array}\right].$$


It can be shown that if $$p(\mathbf{x})$$ is a multivariate Gaussian distribution with covariance matrix $$\Sigma$$ containing the covariances:

$$\sigma_{ij}=\mathbb{E}(x_{i}x_{j})-\mathbb{E}(x_{i})\mathbb{E}(x_{j}),$$

it is $$\Sigma^{-1}=H(\hat{\mathbf{x}})$$, i.e. the inverse of the Hessian at the maximum yields the covariance matrix. Based on this fact, we approximate $$p(\mathbf{x})$$
around $$\hat{\mathbf{x}}$$ via:

$$p(\mathbf{x})\text{\ensuremath{\approx}}\mathcal{N}(\hat{\mathbf{x}},\Sigma_{\hat{\mathbf{x}}}).$$

Note that if $$p(\mathbf{x})$$ is not actually a Gaussian, the $$\sigma_{ij}$$ are generally smaller than the true covariances

$$\mathbb{E}(x_{i}x_{j})-\mathbb{E}(x_{i})\mathbb{E}(x_{j}).$$

The Gaussian approximation is only valid within the vicinity of $$\hat{\mathbf{x}}$$, and therefore especially useful if $$p(\hat{\mathbf{x}})$$ is very peaked around $$\hat{\mathbf{x}}$$. For distributions coming from estimation procedures this is usually the case when a relatively large amount of data has been collected.

Linear approximation of the transfer function
----

Next we will approximate our functions $$f_{j}$$ which can generally be very nonlinear. We take the first-order (linear) approximation of the Taylor series around $$\hat{\mathbf{x}}$$:

$$f_{j}(\mathbf{x})	=	f_{j}(\hat{\mathbf{x}})+(\mathbf{x}-\hat{\mathbf{x}})^{T}\nabla_{f_{j}}(\hat{\mathbf{x}})+\mathcal{O}(\left\Vert \mathbf{x}-\hat{\mathbf{x}}\right\Vert ^{2})
	\approx	f_{j}(\hat{\mathbf{x}})+(\mathbf{x}-\hat{\mathbf{x}})^{T}\nabla_{f_{j}}(\hat{\mathbf{x}})
	\approx	f_{j}(\hat{\mathbf{x}})-\hat{\mathbf{x}}^{T}\nabla_{f_{j}}(\hat{\mathbf{x}})+\mathbf{x}^{T}\nabla_{f_{j}}(\hat{\mathbf{x}})
	\approx	a_{j}+\mathbf{x}^{T}\mathbf{b}_{j}$$

where we have defined

$$a_{j}=f_{j}(\hat{\mathbf{x}})-\hat{\mathbf{x}}^{T}\nabla_{f_{j}}(\hat{\mathbf{x}})$$

and $$\mathbf{b}_{j}:=\nabla_{f_{j}}(\hat{\mathbf{x}})$$. If we aggregate as follows: $$\mathbf{y}=(y_{1},...,y_{m})^{T}$$, $$\mathbf{a}=(a_{1},...,a_{m})^{T}$$ and $$\mathbf{B}=[\mathbf{b}_{1},...,\mathbf{b}_{m}]^{T}$$, we can write the entire system as:

$$\mathbf{y}\approx\mathbf{a}+\mathbf{B}\mathbf{x}$$

This is a second approximation. We assume that the functions $$f_{j}$$, although generally nonlinear, are almost linear within the range of $$\mathbf{x}$$ values around $$\hat{\mathbf{x}}$$ that are accessible with high probability.


Propagation
---

Generally, if $$\mathbf{y}=\mathbf{a}+\mathbf{B}\mathbf{x}$$ is an affine transformation of the Gaussian-distributed variables

$$\mathbf{x}\sim\mathcal{N}(\hat{\mathbf{x}},\Sigma),$$

then it can be shown that:

$$\mathbf{y}\sim\mathcal{N}(\mathbf{a}+\mathbf{B}\hat{\mathbf{x}},\mathbf{B}\Sigma\mathbf{B}^{T}).

Thus, the covariance matrix of the $$y$$-Variables is given by $$\mathbf{B}\Sigma\mathbf{B}^{T}$$. Of special interest are the variances of the $$y$$ variables which are found on the diagonal:

$$(\mathbf{B}\Sigma\mathbf{B}^{T})_{ii}=\mathbf{b}_{i}\Sigma\mathbf{b}_{i}^{T}$$

We can thus estimate the maximum probability $$\hat{\mathbf{y}}$$ and the covariances $$\Sigma_{\mathbf{y}}$$ of the target variables through Gaussian error propagation without further approximations.


Example
---

We consider again the Boltzmann-distributed particles. Let us assume that we have a Device that allows us to measure the kinetic energy $$E$$ and we are interested in calculating the velocity the particle had. We can make use of the equation $$v=\sqrt{\frac{2E}{m}}$$. However, given that the measuremed value $$\tilde{E}$$ has a measurement error of magnitude $$s_{E}$$ with respect to the true value $$E$$, such that the distribution of $$\tilde{E}$$ is given by:

$$p(\tilde{E}|E)=\mathcal{N}(E,s_{E}^{2}).$$

What can we now say about the error in $$v$$, $$s_{v}$$?

Let us assume we measure a value $$\tilde{E}$$. We first used Bayes inversion in order to write down the probability distribution of $$E$$
in terms of $$\tilde{E}$$:

$$p(E|\tilde{E})	\propto	p(E)p(\tilde{E}|E)
	\propto	\frac{1}{2\pi s_{E}^{2}}\exp\left(-\frac{(E-\tilde{E})^{2}}{2s_{E}^{2}}\right)2\sqrt{\frac{E}{\pi(kT)^{3}}}\exp\left(-\frac{E}{kT}\right)
	\propto	\sqrt{E}\exp\left(-\frac{E}{kT}\right)\exp\left(-\frac{(E-\tilde{E})^{2}}{2s_{E}^{2}}\right)
	\propto	\sqrt{E}\exp\left(-\frac{(E-\tilde{E})^{2}kT+2s_{E}^{2}E}{2s_{E}^{2}kT}\right)
	\propto	\sqrt{E}\exp\left(-\frac{E^{2}kT-2(\tilde{E}kT-s_{E}^{2})E+\tilde{E}^{2}kT}{2s_{E}^{2}kT}\right)
	\propto	\sqrt{E}\exp\left(-\frac{(\sqrt{kT}E-\frac{(\tilde{E}kT-s_{E}^{2})}{\sqrt{kT}})^{2}-\frac{(\tilde{E}kT-s_{E}^{2})^{2}}{kT}+\tilde{E}^{2}kT}{2s_{E}^{2}kT}\right)
	\propto	\sqrt{E}\exp\left(-\frac{(E-\frac{(\tilde{E}kT-s_{E}^{2})}{kT})^{2}}{2s_{E}^{2}}\right)$$


We abbreviate $$m_{E}=\frac{(\tilde{E}kT-s_{E}^{2})}{kT}$$ and obtain:

$$\frac{dp(E|\tilde{E})}{dE}	=	\left(\frac{1}{2\sqrt{E}}-\frac{\sqrt{E}}{s_{E}^{2}}(E-m_{E})\right)\exp\left(-\frac{(E-m_{E})^{2}}{2s_{E}^{2}}\right)$$

which becomes zero for:

$$\hat{E}=\arg\max p(E|\tilde{E})=\frac{m_{E}\pm\sqrt{m_{E}^{2}+2s_{E}^{2}}}{2}$$

of which we choose the positive solution:

$$\hat{E}=\frac{m_{E}+\sqrt{m_{E}^{2}+2s_{E}^{2}}}{2}.$$

Note that for vanishing error $$\hat{E}=m_{E}=\tilde{E}$$.

The variance of $$E$$ in a Gaussian approximation around $$\hat{E}$$ is given by the inverse second derivative at $$\hat{E}$$. Using the abbreviation $$\alpha=\sqrt{m_{E}^{2}+2s_{E}^{2}}$$, we obtain:

$$\sigma_{E}^{2}=\left(\left.\frac{d^{2}p(E|\tilde{E})}{dE^{2}}\right|_{\hat{E}}\right)^{-1}	=	\frac{s_{E}^{2}\sqrt{2m_{E}+2\alpha}}{2\exp(-\frac{(\alpha-m_{E})^{2}}{8s_{E}^{2}})\alpha}$$

Thus, we have approximated:

$$p(E|\tilde{E})\approx\mathcal{N}(\hat{E},\sigma_{E}^{2}).$$

Now we use the equation $$v=\sqrt{\frac{2E}{m}}$$ which is linearized by:

$$v(E)	\approx	\sqrt{\frac{2\hat{E}}{m}}+\sqrt{\frac{1}{2m\hat{E}}}(E-\hat{E})
	\approx	\sqrt{\frac{2\hat{E}}{m}}-\sqrt{\frac{\hat{E}}{2m}}+\sqrt{\frac{1}{2m\hat{E}}}E
	\approx	\sqrt{\hat{E}}\left(\sqrt{\frac{2}{m}}-\sqrt{\frac{1}{2m}}\right)+\sqrt{\frac{1}{2m\hat{E}}}E$$

And hence

$$\sigma_{v}^{2}	=	\left(\frac{dv}{dE}\right)^{2}\sigma_{E}^{2}=\frac{s_{E}^{2}\sqrt{2m_{E}+2\alpha}}{2m(m_{E}+\alpha)\exp(-\frac{(\alpha-m_{E})^{2}}{8s_{E}^{2}})\alpha}$$

if we take $$m=1$$ unitless then

$$\sigma_{v}^{2}=\frac{s_{E}^{2}}{\sqrt{2m_{E}+2\alpha}\exp(-\frac{(\alpha-m_{E})^{2}}{8s_{E}^{2}})\alpha}$$

For small errors $$s_{E}$$, this is approximately:

$$\sigma_{v}^{2}\approx\frac{s_{E}^{2}}{2\tilde{E}^{3/2}}$$
