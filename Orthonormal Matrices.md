## What it is?
Summation of elements in rows or columns equal to 1. 

## What is it used for?
Angle between two different vectors is preserved. Therefore, used for the following operations:
- Rotation
- Reflection

## Special Property - $VV^T = I$
If V is from SVD, and I sample the top-p eigenvectors then $V_pV_p^T \neq I$ or $V_pV_p^T \neq I_p$
This is because orthonormality breaks as soon as the top-p eigenvectors are kept. 
However, $VV_p^T = I_p$.

## Special Property - Determinant = +1 or -1
The determinant is always 1 or -1
For more intuition: [[Determinants]]
