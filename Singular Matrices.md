## Intuition:
- Collapses a higher dimensional space to a lower dimensional space. 
	- Note that rectangular matrices also do that and therefore singularity does not apply to rectangular matrices.
- It squishes at least one dimension 
- Since one of the dimension is redundant, transformation by a singular matrix will result in loss of dimensionality. 

## Singularity does not apply to [[Rectangular Matrices]]
- A rectangular matrix can be low rank. Say $A$ is $m \times n$. Then rank, $r = min(m,n)$.
- Say $m < n$, then the rank of $A$ is $m$. 
- A vector of size $n \times 1$ gets squished to $m$-dimensions.
- So information gets lost.

## Special Case:
### Linear Dependency between columns/rows in $A$:
- One of the dimension is redundant
- $A$ is low rank
- $A$ is a singular matrix 
- Also read [[Determinants]] for more intuition

### Are all low rank matrices singular matrices?
No. 

### Are all singular matrices low rank?
Yes.
