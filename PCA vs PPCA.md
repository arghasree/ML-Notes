## Why was there a need for PPCA? How is it better/different from PCA?

The goal of both PCA and PPCA is to find important latent factors.

PCA assumes that if one column is $x_1$, then the other column always has a perfect linear relationship with it, for example $x_2 = w x_1$. 
However, real data does not capture this perfect relationship. It has some noise: $x_2 = w x_1 + noise$

PCA cannot directly cater to this noise. 

## What PPCA does?
### Intuition:

In PCA:
$h$ - of p dimensions -  how much each of the latent vectors are scaled
$D$ - of p x d dimensions -  how each of the latent vector is represented in the d-dim
In PCA, $h$ is fixed, or how much you scale to get back $x$ is fixed
In PPCA it is not. 

In PPCA: 
>$h$ 
>p dimensions - has a probability distribution. 
>The probability distribution is fixed and assumed to be a Gaussian. 
>However the parameters of this distribution $(\mu, \sigma^2)$ are not.
>These parameters are decided by looking at the data.
>These parameters are found out by doing MLE.

> D
> p x d dimensions - is fixed as in PCA
> How is D computed. 
> D is fit to the data **via maximum likelihood**, but the final D will **coincide** (up to scaling/rotation) with the top p principal components of the data—just as in regular PCA.

### After having a prior on $h$, why is it necessary to do a MLE?
$h$ tells you about how much each latent factor is scaled to produce the final X. 
The prior on h needs to be learned based on the data we observe.
Data, X provides the evidence about our assumptions of $h$ and $D$. 

Why MLE?
- MLE has some nice properties, such as it guarantees convergences to the true values of the parameter given enough data. 
- In this way it provides a clear objective. 

Also See: 
	**Question**: Using MLE can we decide if one random variable has an effect on another random variable? Are there other methods that do that?
	Find in: [[MLE and relationship between Random Variables]]

### How PPCA actually work?
