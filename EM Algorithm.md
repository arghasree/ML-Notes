## Where is this algorithm used?
EM Algorithm is used in conditions where (1) the data comes from **different distributions** and (2) we do not know which data comes from which distribution. 

### What does the data record then?
- The data does not contain information about its distribution. 
- Instead the data, (or random variable $X$) contains outcomes about identical events. For example, event: Scores for Test 1. Students from grade 1 will have a distribution of $X$, and students from grade 2 will have a different distribution of $X$, so much so that you may say they are different random variables. This is because the observed values depend on some **additional unobserved variable**. 
- Therefore the data observed is still a random variable. 
- But the parameters required to understand the distribution of this random variable has an extra parameter that describes some latent variable as well. 

### Does including the latent variable increase the parameter space by 1?
- More explanation: Do we assume the data is from a single distribution, say the number of parameters to describe this distribution is 1, plus an additional parameter for the latent space?
- No. 
- The latent variable decides which distribution $X$ belongs to. 
- So as the number of distributions are more than one, the parameters required to describe them also depends on the total number of distributions, and therefore increase. 

### Why is the latent variable associated with some probability?
- To account for uncertainty: We do not know initially which distribution some data belongs to. 

## Why is this algorithm used? Why can't we directly use MLE? (MLE is the 2nd step of this algorithm)

- Why we use MLE?
	- MLE is maximizing the likelihood $p(x_i|\theta)$ where $\theta$ is the parameter of the assumed distribution. 
	- Here we assume that the distribution is constant or only one. 
	- We do not assume that the data comes from multiple distributions. 
- Here the initial assumption that the data comes from a single distribution is questioned. 
- Note that we still **assume** that the distribution comes from $m$ (=constant) number of distributions. 
- Therefore we take an expectation over these $m$ distributions. 
- In other words, the MLE step depends on which distribution is belongs to. If we assume/ the likelihood of $x_i$ belonging to distribution 1 is lower, then the updates (for the parameters of distribution 1) will be reduced. 

## Why is EM iterative?
TO DO 

## Intuition for the E-step 
- Each data point has a membership to each distribution. 
- If the total number of distributions is $m$, then the probability that the data point $x_i$ belongs to distribution $k$ is $p_t[i,k] = p_t(\text{belongs to} = k| x_i, \theta_t)$
- Here we **assume** that the distribution parameters are already available to us and are observed/constant. We also **assume** that the number of distributions is constant (=$m$). 
- Also note that $m$ here denotes the number of latent variables/categories combining which produce the final $X$. 
- Note that these parameters are subject to change but not in this step. Here we assume a distribution with parameters $\theta_t$.
- Here we are only concerned about membership to the $k$ th distribution. 

### Some maths
$$p_t[i,k] = p_t(\text{belongs to} = k| x_i, \theta_t)=\frac{p(x_i​|z_i​=k,\theta_t)  p(z_i​=k|\theta_t)​}{p(x_i|\theta_t)}$$
... by [[Bayes' Rule]]

What each term means:
1. $p(x_i​|z_i​=k,\theta_t)$: Assume we already know the data comes from the $k$ th distribution with $\theta_t$ parameters. Then what is the likelihood that the data comes from such a distribution. 
2. $p(z_i​=k|\theta_t)​$: The probability of the $k$ th distribution: How likely is the $k$ th distribution (if each distribution has parameter values $\theta_t$). This is also given by $w_k$. 
3. $p(x_i|\theta_t)$: Here the latent variable is integrated out. So this is the likelihood that x belongs to any of the distributions with given parameters. 

What is the difference between $p_t[i,k]$ and $w_k$?
- $p_t[i,k]$ is the membership of a data sample in distribution $k$
- $w_k$ is how likely a certain distribution $k$ is among all $m$ distributions.
- Note $p_t[i,k]$ is high only if $w_k$ is high.

What the formulae means intuitively?
- The probability that a sample belongs to certain distribution is:
	- directly proportional to the likelihood of it 
	- directly proportional to how likely the certain distribution is
	- inversely proportional to how likely the sample is to exist in any of the distributions: So if $x_i$ is super common, then the likelihood of $x_i$ increases, but the likelihood of $x_i$ belonging to distribution $k$ decreases. So $x_i$ could be part of other distributions as well. 
- $p(x_i|\theta_t)$ can also be thought of the total probability or a normalization term 

$$p(x_i|\theta^{(t)}) = \sum_{k=0}^{m} w_j^{(t)} p(x_i|\theta_k^{(t)})$$
Substituting ... $$p_t[i,k] = p_t(\text{belongs to} = k| x_i, \theta_t)=\frac{p(x_i​|z_i​=k,\theta_t)  p(z_i​=k|\theta_t)​}{\sum_{k=0}^{m} w_j^{(t)} p(x_i|\theta_k^{(t)})} = \frac{p(x_i​|z_i​=k,\theta_t)  w_k​}{\sum_{k=0}^{m} w_j^{(t)} p(x_i|\theta_k^{(t)})} $$
### Distance encoded in the E-step
- We **assume** that in the E-step, the probability distributions are Gaussians. 
- $x_i \sim \sum_{k=1}^{m}w_k\mathcal{N}(\theta^{(t)}_k) = \sum_{k=1}^{m}w_k \mathcal{N}(\mu^{(t)}_k, \Sigma^{(t)}_k)$ where $m$ is the number of Gaussians. So $x_i$ is sampled from a distribution where $\mu^{(t)}_k \in \mathbb{R}^d$ 
	- Note that $\Sigma_k \in \mathbb{R}^d$ with diagonals = non-zero. 
	- Non-diagonal elements with non-zero element suggests feature correlation (linear relationship) in all $X$. 
- When we measure the membership of $x_i$ to the Gaussian component $k$, we do: 
$$p_t[i,k] =\frac{p(x_i​|z_i​=k,\theta_t) w_k​}{\sum_{k=0}^{m} w_j^{(t)} p(x_i|\theta_k^{(t)})}$$
- Here $p(x_i​|z_i​=k,\theta_t)$ is a Gaussian as $p(x_i)$ is Gaussian and $x_i$ was sampled from a Gaussian (mixture of Gaussians to be precise) 
- The term $p(x_i​|z_i​=k,\theta_t)$ basically tells you **how far away** $x_i$ is from $\mu^{(t)}_k$, thus the concept of distance. 
- Instead of using an Euclidean distance, other distances can be used. 
- Why is the distance so important?
	- Here for different distance metrics, the similarity between $x_i$ and distribution $k$ would be different. This would make $p(x_i| ... )$ different, resulting in different memberships. 

**More on difference between Gaussian and Euclidean:** $$K(x,x') = \text{exp}(\frac{-||x-x'||^2}{2\sigma^2})$$
	The kernel function **decreases** with distance and ranges between zero and one. In euclidean distance, the value **increases** with distance. Thus, the kernel function is a more useful metrics for **weighting** observations.
	The fact that it's bounded between zero and one is a nice property, whereas the absolute distance (it can be anything) in Euclidean distance can cause instability and difficulty in modeling.
	Euclidean distance (without the negative sign) is not a similarity measure, it's a distance function. The gaussian kernel is a similarity measure.
	You can think the Gaussian kernel like a normalization function for Euclidean distance.
	
## Intuition for the M-Step 


# Problems with using EM for generative models:
- The number of mixtures need to be pre-determined: Can't be too less or too more
- For a very complex dataset, the number of distributions need to be very large 
-  In the E-step, membership of each datapoint to each of the $m$ clusters is measured. 
	- A notion of distance comes: if the datapoint is closer to $k$ th cluster, then $p[i,k]$ is higher.
	- Therefore different distance metrics result in different generative models.
	- Euclidean distance might not be a good measure to measure similarity of $x_i$ with distribution $k$. 
