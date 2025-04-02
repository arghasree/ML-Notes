Here some rectangular matrix, $X$ is a collection of data points having the same features, $x_i \in \mathbb{R}^d$.
Covariance matrix $\Sigma = X^TX$ 
	Why? If mean of $X$ is 0, then Covariance = $(X-0)^T(X-0)$ 
$X$ has $d$ axes, along which it has some associated real numbers that explain the behavior of the $d$ th dimension. So the covariance matrix measures the variance of data in each of these dimensions. 
It also measures pairwise dependencies across dimensions. 

# Eigenvector:
- There is a vector, $v$ (of the same dimensions as $X$, $v \in \mathbb{R}^d$) that upon a transformation from matrix $\Sigma$, we get back a scaled vector ($\lambda v$).
$$\Sigma v = \lambda v$$
- This vector is the eigenvector of the covariance matrix of $X$. 
- $X$ has $d$ axes, along which it has some associated real numbers that explain the behavior of the $d$ th dimension. 
-  $\Sigma v$ gives a $d \times 1$ vector, $\lambda v$, which is the same vector but scaled. So there is no rotation of the vector, it is only scaled. 
- The "action" of the covariance matrix in that direction is purely to scale the data, not to change its orientation. 
- This indicates that the direction $v$ is inherent to the structure of the data, capturing a principal axis of variance.

# Eigenvalue:
If $v$ is an eigenvector of the covariance matrix $\Sigma$ with eigenvalue $\lambda$, then $$\lambda = v^T \Sigma v$$
- Now visualize $X$ scattered across the $d$ dimensions. 
- The first eigenvector $v$ (that get get from $\Sigma$) is superimposed on the d-dim map of X where the data $X$ has most variance. 
- In that direction, how much variance $X$ has is given by the associated $\lambda$. 
- Say there is a eigenvector $v$, and the sum of the squared error (SSE) for each datapoint $x_i$ from $v$ is measured. 
- The first principal component should have the least SSE. 
- But is eigenvalue for $v$ = = SSE? No. 
- Say it has the least SSE for 15 out of 18 points, then that means that 15/18=0.83 variance is retained. Eigenvalue is related to this. Higher the eigenvalue, more number of samples can be explained using the corresponding eigenvector.  




