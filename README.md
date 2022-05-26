# Optical flow with Kalman filter
Python code that uses optical flow for tracking a pre-recorded video with Kalman filter to filter the results of optical flow. The optical flow code has been adopted from this [link](https://www.geeksforgeeks.org/opencv-the-gunnar-farneback-optical-flow/).
The code works on a pre-recorded video. So, make sure to have a recorded video in the same folder as the code before executing it.
The Kalman filter equations have been adopted from the works of Greg Welch and Gary Bishop from their paper titled: <em>`An Introduction to the Kalman Filter'</em> [1].  
For integrating the Kalman filter with the optical flow for tracking, the following state equations have been used:

$x\_{k+1} =  \\underbrace{\\begin{bmatrix}1 & \\Delta t  \\\\ 0  & 1 \\end{bmatrix}}\_{A}   \\begin{bmatrix}p\_{x}^{i}  \\\\ p\_{u}^{i}  \\end{bmatrix} + \\underbrace{\\omega\_{k}}\_{\\textrm{process noise}}$


$y\_{k}^{i} = \\underbrace{\\begin{bmatrix} 1  & 0 \\\\0 & 1 \\end{bmatrix}}\_{H}\\begin{bmatrix}p\_{x}^{i}  \\\\ p\_{u}^{i}  \\end{bmatrix} + \\underbrace{v\_{k}}\_{\\textrm{measurement noise}}$
where state
$x\_{k+1}^{i} = \\begin{bmatrix} p\_{x\_{k+1}}^{i}  & p\_{u\_{k+1}}^{i}\\end{bmatrix}^{T}$ and the measurement *y*<sub>*k*</sub><sup>*i*</sup>
is the measurement of the output received from optical flow.

The typical Kalman equations are:

Measurement update equations:

*K*<sub>*k*</sub> = *P*<sub>*k*</sub><sup>−</sup>*H*<sub>*k*</sub><sup>*T*</sup>(*H*<sub>*k*</sub>*P*<sub>*k*</sub><sup>−</sup>*H*<sub>*k*</sub><sup>*T*</sup>+*R*<sub>*k*</sub>)<sup>−1</sup>

*x̂*<sub>*k*</sub> = *x̂*<sub>*k*</sub><sup>−</sup> + *K*<sub>*k*</sub>(*z*<sub>*k*</sub>−*H*<sub>*k*</sub>*x̂*<sub>*k*</sub><sup>−</sup>)

*P*<sub>*k*</sub> = (*I*−*K*<sub>*k*</sub>*H*<sub>*k*</sub>)*P*<sub>*k*</sub><sup>−</sup>


Time update equations:

$\\widehat{x}\_{k+1}^{-} =   \\begin{bmatrix} \\widehat{p}\_{x\_{k+1}}^{(i)-}  \\\\ \\widehat{p}\_{u\_{k+1}}^{(i)-}\\end{bmatrix} =  \\begin{bmatrix}
  1 & \\Delta t \\\\ 0 & 1
\\end{bmatrix}  \\begin{bmatrix} \\widehat{p}\_{x\_{k}}^{i}  \\\\ \\widehat{p}\_{u\_{k}}^{i}\\end{bmatrix}$

*P*<sub>*k* + 1</sub><sup>−</sup> = *A*<sub>*k*</sub>*P*<sub>*k*</sub>*A*<sub>*k*</sub><sup>*T*</sup> + *Q*<sub>*k*</sub>
The intial values were taken to be:
$x\_{o} = \\begin{bmatrix} random()\\\\ 0 \\end{bmatrix}$,
$P\_{o} = \\begin{bmatrix}
  1 & 0 \\\\ 0 &1
\\end{bmatrix}$
## References:
[1] [Welch, G. and Bishop, G., 1995. An introduction to the Kalman filter](https://perso.crans.org/club-krobot/doc/kalman.pdf).
