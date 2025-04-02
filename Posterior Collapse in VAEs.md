First some recap on VAEs.

In VAEs, there is an encoder part and there is a decoder part.

Here is the [[Connection between classification and encoder of VAEs]] and some intuition about why the KL-divergence loss is needed in VAEs

# Posterior Collapse

- When KL divergence loss tends to 0, even during training it is like saying we sample a random noise $h$ and then make up an X. There is no true relationship between h and x.
- This becomes dangerous because then during training, by only using the reconstruction loss, it learns W such that x can be reconstructed.
- So randomness produces reasonable x.
- How?
- W becomes such that the x is memorized. h is completely ignored.
- This is dangerous. It is same as saying that we do not need a recipe. We remember how to arrange components to produce a final result. So the number of final results is limited (as it is memorized and therefore depend on the size of the decoder network.)
- **Solutions**?
    - Use a **weaker decoder** so it needs information from h.
    - Reduce weight to the KL divergence loss during training.
- Example intuitions:
    - From a book, instead of a meaningful summary, the decoder predicts “It was a good book.” Very generic, applicable to most x.
    - From different 3s in the MNIST dataset, only a fixed 3 is output.
- How memorization works?
    - In the reconstruction term, $\frac{1}{n}\sum_{n}^{i=1}||X_i - \hat{X_i}||_2^2$ wants to reduce this term.
    - So if $\hat{X_i}$ learns a little bit of all the $X_i$, i.e., the average of all samples, then the average difference will reduce.
    - This is a shortcut.
    - Say $X_i = Wh+b$ where $W=0$ and $b = \text{average}(X)$, then the most common sample of the X has been memorized, or a $\hat{X_i}$ has been memorized that looks a little bit like all the X.
    - Here the loss term would be stuck and very little changes would happen to the loss term in each epoch.