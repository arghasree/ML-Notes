## Intuition:
- Represents the factor by which areas (in 2D matrices) and volumes (in 3D matrices) change after undergoing transformation by the matrix $A$. 
- The determinant is directly related to how a matrix **scales** space.

For example:
If the determinant of $A$ is 2, then a space transformed by $A$ now occupies twice the space it did before. 

## Orthonormal Matrices:
Determinants of [[Orthonormal Matrices]] = 1 or -1 as they only rotate the space and do not scale the space.

### Rectangular Matrices:
- We do not have determinants of Rectangular matrices. 
	*Reason*: The geometric meaning of the determinant is by how much its corresponding linear transformation changes the volume of the unit n-cube. If you have a non-square matrix, the resulting figure would exist in a space with a **different number of dimensions**, making any **comparison** between **volumes meaningless**.
- $Det(A) = 0$ in this case

### Square Matrices with linear dependencies:
- Linear dependencies also squishes the space into low dimensional space than the total number of columns or available dimensions. 
- $Det(A) = 0$ in this case