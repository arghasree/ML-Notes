### What is the **loss landscape**, and how is it related to the feature space?
- The feature space: There are possible values of feature 1. There are possible values of feature 2. 
- For each such pair, there are two parameters that decide the contribution of each feature to the output.
- X is the feature space.
- Therefore, the x axis is for possible values of parameter 1, and the y-axis is for possible values of parameter 2.
- For each such combination of the parameters, there will be a loss value. This creates the loss landscape. 
- The loss landscape is a surface over the parameter space.  It does not have its own dimension.
- The gradient gives the direction of steepest increase of the loss function


### If two features are orthogonal, what does the loss landscape look like?
- If two features are orthogonal, changes on one will have no effect on the loss due to the other feature change. That is, $\frac{\partial L}{\partial w_1}$ will be constant when we change $w_2$. 
- $\frac{\partial }{\partial w_1}( \frac{\partial L}{\partial w_2})$ gives us how on changing $w_1$, the rate of change of loss wrt $w_1$ changes. It does not, as changing $w_1$ has no effect on how $w_2$ changes loss. In other words, even if you change $w_1$, the loss function will not change its rate of change due to $w_2$.  
- So $\frac{\partial }{\partial w_1}( \frac{\partial L}{\partial w_2})$ will be 0, in other words the off-diagonal elements of the Hessian matrix will be 0. 
- The loss landscape is symmetric. 
- When the loss is not dependent on a combination of features, the loss function can be expressed as $L = f(w_1) + g(w_2)$ 
- When the loss is dependent on a combination of both the parameters, then the loss function can be written as $L(w_1, w_2) = \lambda_1 w_1 ^2 + \lambda_2 w_1w_2  + \lambda_3 w_2 ^2$ ([Desmos Link](https://www.desmos.com/3d/15dhozbkq8))
- In the previous expression, $w_1w_2$ is another feature, which is a combination of already present features.
- The moment $\lambda_2$ is greater than 0, it skews the graph into an ellipsoid form. 
- The skew would also occur if $\lambda_3 = 0, \lambda_2>0$  
- Also note, the skew would not happen if it was a linear combination of $w_1$ and $w_2$. It had to be a non-linear combination. ([Desmos Link](https://www.desmos.com/3d/sgegyymzgz))
- Note that in linear regression, the loss function can be described as: $$L = \sum_{i}^{n}(X_iW - Y_i)^2$$ where $X_i, W \in \mathbb{R}^d$, so $$L = (w_1X_{i1} + w_2X_{i2} + .. + w_dX_{id} - Y_i)^2$$
- So we assume the loss function is a linear function of each dimension with no feature ($X_{ij}$) dependent on each other. 
- If $w_1=w_2$, then it is a circular contour. If $w_1 \neq w_2$  then it is also an ellipsoid but the contours are aligned to the x and y axis. However, in case of non-linear combinations, the axis is rotated ([Desmos Link](https://www.desmos.com/3d/7w41gx1apk)) 
- In the later case, GD will update one dimension with larger updates than the other. So the gradient will focus on $X_{i1}$ more than $X_{i2}$ if $w_1>w_2$. 

### If the two features are not orthogonal, what do the gradient updates look like?
- [Desmos Link](https://www.desmos.com/3d/ijjfj0ev5e)
- The gradient on one dimension is dependent on the other dimension. 
- So $w_1 = w_1 - \nabla_{w_1}L$  and as $w_2$ is dependent on $w_1$, so when calculating $w_2 = w_2 - \nabla_{w_2}L$, $\nabla_{w_2}L$ has $w_1$ terms. Note that changes on both parameters are simultaneous and use the old value of $w_1$.
- Also note the gradient is linear for a quadratic loss function. 
- The Hessian provide extra information while doing Gradient descent updates. 
- While the first-order updates are flawed, the second order gradient updates are better as the inverse of the Hessian provides extra information to correctly update the parameters. 
- Even if the features are correlated, how does the Hessian correct those updates?
- This happens because in first order updates:
 ![[Pasted image 20250219162319.png]]
- And in second order updates:
![[Pasted image 20250219162420.png]]
- The second order updates keep in mind the first order updates for other parameters as well. As they are dependent, this provides a better estimate of the parameter updates.
- Instead of treating parameters **independently**, second-order updates **jointly adjust them** based on their relationships.