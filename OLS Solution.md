## The OLS solution:
$W_{MLE}= (X^TX)^{−1}X^TY$

## Problems with this solution:
- Unstable if $X^TX$ is invertible (See [[Matrix Inverse]]) 
- When is $X^TX$ invertible?
	1. Linear dependency between features 
	2. Duplicate rows
	3. Less data (not enough data to exhibit independence between features)
- When is $X^TX$ ill-conditioned?
	- When the condition of $X^TX$ is very high (near linear-dependency)(See [[Condition]])
- Causes $X$ to be low rank
- 