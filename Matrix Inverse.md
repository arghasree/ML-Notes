### Intuition:
- If there is a matrix $A$, the corresponding transformation will change the space by scaling and rotating. 
- Inverse is bringing it back to the original space.
- Not all transformed spaces can be inverted back to its original form. 
- Therefore rectangular matrices cannot be inverted. 
- And when $A$ is invertible, it preserves information about all the dimensions.

### Inverting matrices
$(ABCD)^{-1} = D^{-1}C^{-1}B^{-1}A^{-1}$
$(ABC)^{-1} = C^{-1}B^{-1}A^{-1}$
$(AB)^{-1}=B^{-1}A^{-1}$

### Special Case of [[Rectangular Matrices]]:
They cannot be inverted as dimensionality loss occurs when a space is transformed to another by a rectangular matrix. 

### Special Case of Square matrices with linear dependency:
- Loss of dimensionality also occurs in [[Singular Matrices]].
- Such matrices, such as projection matrices, squish information to lower dimensions. 
- Also related to [[Determinants]]: When determinant is 0, $A$ is invertible. 

