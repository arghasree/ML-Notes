## Covariate Shift
What happens when we do generalization, and the data is dissimilar for training and testing. 
We assume we have some outcome space, X and you decide the scope. 
Example: X = all patients in Edmonton 
In the training setting, during clinical trials, $p_{train}$ has mostly young people/students, fewer from the general population. 
During deployment, $p_{test}$ has mostly general population, older sick people. 
This is no-coverage 
## Non-stationary points
What if the model changes, $p(y|x)$ changes? 
$p_{train}(y|x) \neq p_{test}(y|x)$ 
$f(x)$ changes
For example, y = pump speed, x = {desired temp, temp outside, ... }
Training new system and test if the pump gets clogged. 
x = desired temperature - temperature inside 
Relationship between y and x is given as a curve
The relationship is modeled by $f^*(x)$
$f^*_{true}$ during training is modeled by a different function 

One solution: Always update on the new data and down-weight the old data  

## Generative Models
Learn a complex distribution to sample from $p(x)$ to sample from.
- In contrast, exponential families model $p(y|x)$, and this is not a complex distribution. 
- So the relationship was not complex to begin with. 
- **Uses**: LLMs, Diffusion models, RL models, simulators for robotics, data privacy etc.
- **Goal**: Accuracy and usability. 
	- Learn accurate $\hat{p}(x)$ from true $p(x)$
	- Learn $\hat{p}$ that is efficient to sample from 

### Simplest Complex Distribution:
Mixture models $x \in \mathbb{R}^d$
$p(x) = \sum_{k=1}^{m} w_k p_k$ where $w_k \ge 0$ and $\sum_{k=1}^{m} w_k = 1$ 
$p_k$ is a pdf or pmf and sampling from it is easy. 
### Sampling from p
1. Sample component $k \sim p(k) = w_k$
2. Sample $x \sim p_k$

When we sample we sample from $p(x)$
How do we sample from a Gaussian distribution etc. 
Generates from k th distributions $w_k$ number of times

Why do we get this structure?
Reason: Multimodality: hidden variables
$x = [\text{house temp, humidity}]$ 
z = window open
Why am I sampling from this region vs why am I sampling from the other region?

### Learn mixture models
We learnt coefficient, 
$\theta = (w_1, w_2, .. w_m)p(x|\theta_k)$; $\theta_k = (\mu_k, |sigma_k^2)$ for Gaussian components
$D = \{x_i\}^n_{i=1}$ What is $\hat{p}$? 
$\hat{p}$ is the MLE.
$$min_{\theta} -\ln p(D|\theta) = \sum_{i=1}^{n} -\ln p(x_i|\theta) = \sum_{i=1}^{n} -\ln [\sum_{i=1}^{n} w_k p(x_i|\theta)]$$
### EM Algorithm:
Introduce auxiliary variable $p(z=k|x)$ probability of x coming from component $k$. 
Iterate and alternate between optimizing $\theta^{(t)}$, and $p_t$
**E-step** = Compute $p_t[i,k] = p[z_i=k|x_i, \theta^{(t)}]$ = 
We have $p(x|\theta^{(t)}) = \sum_{k=1}^{m}p(x|\theta_k^{(t)})$
..
Cycle through all samples $i, k \in \{1,...m\}$ to calculate $p_t[i,k]$.

**M step**: 