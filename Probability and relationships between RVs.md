# Probabilities can be used to find the relationship between different Random Variables. How?

Probabilities help us calculate how **likely** two events are. 
## The kind of relationship that probability can quantify is:
- Mutual Independence (Using joint probabilities or conditional probabilities)
- Correlation and Covariance - Linear relationship
- Mutual Information - Non-linear relationship
- Conditional dependencies in graphical networks 

Also See:
	[[MLE and relationship between Random Variables]]

## How can I say that two random variables are independent?
Say I have 2 random variables $X$ and $Y$.
$X$ has some probable values it can take, so does $Y$. 
If they are independent, when $X$ observed, it will have an effect on $Y$. 
For independent events, $P(X,Y) = P(X)P(Y)$ 
### Cartesian Product
Say $X$ has values $\{x_1, .., x_d\}$ and $Y$ has values $\{y_1, .., y_p\}$, then the joint sample space comprises all pairs of $X$ and $Y$: $(x_i,y_i)$. This is also called the Cartesian Product. 

But this has **no relation** to how the probability is distributed among each pair. They are independent only if the probability factorizes into individual probabilities like $p(x)$ and $p(y)$.
$P(X=x_i​,Y=y_j​)=P(X=x_i​)P(Y=y_j​)$
