## Classification
When we perform a classification task, the goal is to find a link between input random variable X and another observable random variable Y. 
This `link` or relationship can be modeled by a linear model with weights W. In turn we therefore learn the `link` given by the probability distribution $p(y|x,w)$. Here $w$ is also a variable and is learnable, but is not observed. The goal is to derive Y from X somehow. 
Here X has its own distribution, $p(x)$.

## Generation
- When we talk about generating, we are generally talking about generating $X$, and therefore we try to model $p(x)$.
- Previously we did not worry about where X comes from. We were busy thinking about where Y comes from. We believe Y comes from X and we try to understand their relationship. 
- Also note that previously X and Y came in pairs. So $x_i$ has a corresponding $y_i$.
- Here however, we try to model X. Each $x_i$ has to be similar to the observed X. 
- Here we do not have to understand a relationship between a certain other random variable, and X. 
- To make a new $x_i$, we need to know what the recipe and the ingredients.
- But would a recipe suffice? Wouldn't we have to know the ingredients? 
- For example, if we have an image of a person's face, what are the components? 
- We know the shape or form of what we are creating, i.e., the dimensions of the image. 
- But what about the components? In a 32 x 32 image, there are $32*32=1024$ dimensions. Are these the components?
- If we assume we have different choices of these 1024 dimensions, we are are assuming each of these components are independent. Maybe they are not. If they are not, then we have to find the components/directions which have maximum variance in that direction (by going through all data samples), and only take the top $p$ directions. 
- This is also given by the D matrix. D captures information about the whole X and examines which of all components of X are really important. 
- In other words, D is the set of components in X's language (as it is a $p \times d$ matrix). 
- So now we have $p$ components. How much of the individual components do we consider? In other words what is the magnitudes of each of these principal axes? 
- This is given by h. This is the recipe and this can change. 
- In the image example, we can think of this as what is the value of the pixel? If the pixel value is $a$ for some component, then it will be $a$ for other dependent components as well. 
- This is how we can form something similar to X from different variations of the same components captured by X. 
- (Another example) In other words, if a person is introverted, then the new person is also introverted with a different degree of introverted-ness. 

## Link between the two
- In classification, we did not worry about where X comes from. We were busy thinking about where Y comes from. We believe Y comes from X and we try to understand their relationship. 
- Also note that previously X and Y came in pairs. So $x_i$ has a corresponding $y_i$.
- In generation however, we try to model X. Each $x_i$ has to be similar to the observed X. 
- In generation we do not have to understand a relationship between a certain other random variable, and X. 
- In generation we learn a combination of different components that result in $x_i$. 
- To learn different components of $x_i$, we go through other examples of $x_i$ and the whole of X. 
- As there is no perfect answer to the generation process, there is no corresponding $x'_i$. In the prediction process, there was a corresponding $y_i$ to the $x_i$, therefore there we knew the components, we needed to know the perfect way to combine them. So we learned $w$. 
- In the generation process, we do not know the components, which we learn from X, and then generate using any combination of these components, as there is no perfect answer to the generation. 