Time-lagged independent component analysis (TICA)
====

Literature: 
---

* Pérez-Hernández, G. Paul, F., Giorgino, T., De Fabritiis, G. and Noé, F.: Identification of slow molecular order parameters for Markov model construction. **J. Chem. Phys.** 139, 015102 (2013); doi: 10.1063/1.4811489
* Schwantes, C. R. and Pande, V. S., Improvements in Markov State Model Construction Reveal Many Non-Native Interactions in the Folding of NTL9. **J. Chem. Theory Comput.** 9, 2000 (2013).
* Molgedey, L. and Schuster, H. G., Separation of a mixture of independent signals using time delayed correlations. **Phys. Rev. Lett**. 72, 3634 (1994).

Time-lagged or time-structure based independent component analysis
---

We consider a $$ d $$-dimensional vector of input data, called $$ \mathbf{r}(t)=(r_{i}(t))_{i=1,...,D}$$. Here, $$ t $$ is an integer from $$ \{1...N\} $$ denoting the time step. We assume that the data is mean-free, i.e. from a general input vector $$ \tilde{\mathbf{r}}(t) $$, we first obtain: 

$$ \mathbf{r}(t)=\tilde{\mathbf{r}}(t)-\langle\tilde{\mathbf{r}}(t)\rangle_{t} $$

where $$ \langle\tilde{\mathbf{r}}(t)\rangle_{t} $$ is the data mean. We first compute the covariance matrices from the data: $$ c_{ij}(\tau)=\langle r_{i}(t)\: r_{j}(t+\tau)\rangle_{t} $$ where $$ \tau $$ is the lag time. We will need two matrices for TICA, for the choices $$ \tau=0 $$ and another positive value of $$ \tau $$. $$ \langle\cdot\rangle_{t} $$ denotes the time average. We can evaluate it as follows: 

$$ c_{ij}(\tau)=\frac{1}{N-\tau-1}\sum_{t=1}^{N-\tau}r_{i}(t)\, r_{j}(t+\tau). $$

It is easy to verify that $$\mathbf{C}(0) $$ is a symmetric matrix. For algebraic reasons we will need that  $$ \mathbf{C}(\tau) $$ is also symmetric, which is not automatically guaranteed when estimating it from a finite data set. Therefore we enforce symmetry from a data-computed matrix $$ \mathbf{C}_{d}(\tau)$$:

$$ \mathbf{C}(\tau)=\frac{1}{2}\left(\mathbf{C}_{d}(\tau)+\mathbf{C}_{d}^{\top}(\tau)\right). $$
 
Now we solve the generalized eigenvalue problem: 

$$\mathbf{C}(\tau)\:\mathbf{U}=\mathbf{C}(0)\:\mathbf{U}\:\boldsymbol{\Lambda}$$
 
where $$\mathbf{U}$$ is the eigenvector-matrix containing the independent components (ICs) in the columns and $$\Lambda$$
is a diagonal eigenvalue matrix. This problem can be solved by an appropriate generalized eigenvalue solver (directly).

Now, the data can be projected onto the TICA space:

$$\mathbf{z}^{\top}(t)=\mathbf{r}^{\top}(t)\mathbf{U}$$
 
in this step, we can perform a dimension reduction by selecting only a sub-matrix $$\mathbf{U}$$ consisting of the first $$m$$
columns of the full-rank $$\mathbf{U}$$.

EMMA code
---


    from pyemma.coordinates.tica import TICA

	trajfiles = "*.dcd"	
	topfile = "bpti.pdb"

    tica = TICA(trajfiles, topfile)


Amuse algorithm
---

The generalized eigenvalue problem can be solved in two steps. The two step procedure is called AMUSE algorithm and works as follows:

1. Solve the simple PCA Eigenvalue problem 
$$\mathbf{C}(0)\:\mathbf{W}=\mathbf{W}\:\boldsymbol{\Sigma},$$ 
where $$\mathbf{W}$$ is the eigenvector matrix with principal components and $$\boldsymbol{\Sigma}$$ are their variances (diagonal Eigenvalue matrix).

2. Transform the mean-free data $$\mathbf{r}(t)$$ onto principal components $$\mathbf{y}(t)=\mathbf{W}\:\mathbf{r}(t)$$.

3. Normalize the principal components: $$\mathbf{y}'(t)=\boldsymbol{\Sigma}^{-1}\mathbf{y}(t)$$
 
4. Compute the symmetrized time-lagged covariance matrix of the normalized PCs: $$\mathbf{C}_{sym}^{y}(\tau)=\frac{1}{2}\left[\mathbf{C}^{y}(\tau)+(\mathbf{C}^{y}(\tau))^{\top}\right]$$
 
5. Perform an eigenvalue decomposition of $$\mathbf{C}_{sym}^{y}(\tau)$$ to obtain the eigenvector matrix $$\mathbf{V}$$ and project the trajectory onto the dominant eigenvectors to obtain $$\mathbf{z}(t)$$.

In summary, we can write the transformation equation in three linear transforms:

$$\mathbf{z}^{\top}(t)=\mathbf{r}^{\top}(t)\mathbf{U}=\mathbf{r}^{\top}(t)\mathbf{W}\boldsymbol{\Sigma}^{-1}\mathbf{V}.$$
 
TICA will be used as a dimension reduction technique. Only the dominant TICA components will be used to go to the next step. In order to reduce the dimension, use only a few columns of $$\mathbf{U}$$.

