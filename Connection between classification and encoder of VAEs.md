Inside find the connection and some intuition for the necessity of the KL Divergence loss to learn the encoder. 
# Connection between learning $p(y|x)$ with $q(h|x)$

## Learning $p(y|x)$, a classification task

- We can think of y as a random variable observable with the other features of X.
- In this case as y is a column in X, and is a linear combination of other features of X, the rank of X decreases.
- In case y is non-linearly dependent on the features of X, this problem would cease to exist.
- Overall, we may think of y as a feature of X, (there is always a mapping between X and Y, they appear in pairs).
- During training, we have a set of labels and the corresponding features, which after combining linearly or non-linearly produce the label.
- The goal is to learn some probability distribution, i.e., for given values of X, this is the label. One may think of it as a memorized discrete and sparse distribution.
- But this distribution is not generalizable.
- When we learn the relationship between X and Y through a neural network, we are learning to minimize $- \ln p(y|x,W)$.
- So the parameters of the neural network is $W$ , in other words to learn y, we assume a model with parameters $W$ and then try to increa the likelihood of observing y when given $x$ and $W$. Here the changeable parameters are $W$.
- More about NNs and learning the relationship between X and Y.
    - So to learn the relationship between y and x, instead of directly mapping an if else condition (not generalizable), we assume a model which tries to have different combinations of the features, and while training we learn which combination/magnitude of combination yields y. More the depth of the neural network, more combinations (linear or non-linear) is taken into consideration.
    - More nodes in a layer = More combinations of the features are explored. If a certain combination (including `y=cat` at the end ) is heightened, then we say it is a `cat`.
        - Each of these combinations result in focusing on a different tangible aspect of the input. For example, someone may focus on the good aspects of a situation, someone the bad aspects. Or in an image example, one set of combinations focus on the smile of the image, or the other may focus on the eyes.
        - However, if each of these combination is actually a tangible component, we as humans focus on, is a different argument. We might not see the patterns that the NN sees.
        - **More nodes = more parallel “feature combinations” being tried out at that level.**
    - More layers in a NN = Identifying relationships between different combinations.
        - For example, how is the good aspects of a situation linked with the bad aspects.
        - How is a smile related to the eye.
    - More the variety in the training data, more combinations of the features diverge from one another. In other words, the activation from one node would look very different from the activation of the other node. But if the training data has less variety, for example, all pictures are made of a person not smiling, then the eyes will look the same/ vs a smiling photo will have eyes creased up.
- So instead of learning if-else conditions for the relationships between X and Y, we generalize it by assuming there is a linear or linear combination of X will produce a Y. Therefore we parameterize the problem and solve for $p(y|x)$. We solve by **assuming the presence of a framework that explains y given x.**
- During testing, we assume that this same model explains the new $X$ and $Y$ relationship.
- During testing we again calculate $p(y|x,W)$. Say it is a regression task. We do not know what y is. Instead based on the previously observed X and Y pairs, and the model that we have learned, we approximate the new y. This predicted y might not be/close to the true y though.

## Learning $q(h|x)$, the encoder

- Similar to the previous assumption, we can assume that the latent representation is a part of X.
- Although in the VAE setting we assume h is independent and X comes from h.
- Regardless, the probability $q(h|x)$ will be able to map the relationship between h and x..
- In Generative processes, we assume X comes from Y: $X \sim p(x|y)$
- Similarly here we assume $X \sim p(x|h)$
- But we may flip it into $h \sim q(h|x)$
- Previously, we assumed that there was a model that mapped X to Y by parameterizing this model by W.
- Here we can do the same thing: Assume there is a relationship between X and h, some combination of features of X can lead to h
- So the distribution $q(h|x)$ during testing and generation, assumes the same model learned during training. And then the predicted/generated h might not explain the X. but we assume it does, based on the model and use it for the decoder.
- Why we need to do this for generation?
    - During training, we needed $h$ to learn a mapping between the different values of $h$ and regenerated x.
    - During testing, we give a random h and use the learned mapping to produce a new x.
    - Why use a random $h \sim \mathcal{N}(0, I)$ and not a h sampled from the learned $q(h|x)$?
    - The learned $q(h|x)$ produces a probable h from the input x, here x is not observed.
    - Why use $q(h|x)$ then? During training?
    - Because not all $h \sim \mathcal{N}(0, I)$ produce a reasonable x. It produces all possible values of x. But our dataset/needed x space is much small.
    - So first we learn the proper h from x, then use it to regenerate x.
    - How does a random $h \sim \mathcal{N}(0, I)$ map to the learned decoder to produce a x that looks like the x we learned during training?
    - Although a specific h (think of it like a specific x from dataset cats and dogs) produces the generated images **we want**, the learned decoder expects only h that make up X.
    - What happens when a different h is given to the decoder?
    - When a h that is far away from the h during training, it will give weird x that was not observed during training.
    - To recover from this negative phenomenon, we have the KL Divergence loss.
    - The goal of the KL divergence loss is to make $q(h|x)$ close to $p(h)$, which is the normal distribution. Doing so ensures that during testing, a h is sampled that looks very close to the one sampled during training.
- What happens when the KL divergence loss tends to 0?
    - h sampled becomes very close to the ones during training. And a very realistic x will be generated.
- Loss for the encoder:
	- During training, the encoder depends on learning the KL divergence loss. 
	- Note that we do not have any fixed observable h, so we cannot use other losses such as MSE. 
	- So instead we try to reduce the KL divergence. 
