# Optical flow with Kalman filter
Python code that uses optical flow for tracking a pre-recorded video with Kalman filter to filter the results of optical flow. The optical flow code has been adopted from this [link](https://www.geeksforgeeks.org/opencv-the-gunnar-farneback-optical-flow/).
The code works on a pre-recorded video. So, make sure to have a recorded video in the same folder as the code before executing it.
The Kalman filter equations have been adopted from the works of Greg Welch and Gary Bishop from their paper titled: <em>`An Introduction to the Kalman Filter'</em> [1].  
For integrating the Kalman filter with the optical flow for tracking, the following state equations have been used:

$  x_{k+1} =  \underbrace{\begin{bmatrix}1 & \Delta t  \\ 0  & 1 \end{bmatrix}}_{A}   \begin{bmatrix}p_{x}^{i}  \\ p_{u}^{i}  \end{bmatrix} + \underbrace{\omega_{k}}_{\textrm{process noise}}$

$y_{k}^{i} = \underbrace{\begin{bmatrix} 1  & 0 \\0 & 1 \end{bmatrix}}_{H}\begin{bmatrix}p_{x}^{i}  \\ p_{u}^{i}  \end{bmatrix} + \underbrace{v_{k}}_{\textrm{measurement noise}}$
where state $x_{k+1}^{i} = \begin{bmatrix} p_{x_{k+1}}^{i}  & p_{u_{k+1}}^{i}\end{bmatrix}^{T}$ and the measurement $y_{k}^{i}$ is the measurement of the output received from optical flow.

The typical Kalman equations are:

Measurement update equations:

$K_{k} = P_{k}^{-}H_{k}^{T}(H_{k}P_{k}^{-}H_{k}^{T} + R_{k})^{-1}$

$\widehat{x}_{k} = \widehat{x}_{k}^{-} + K_{k} (z_{k}-H_{k}\widehat{x}_{k}^{-})$

$P_{k} = (I-K_{k}H_{k})P_{k}^{-}$


Time update equations:

$\widehat{x}_{k+1}^{-} =   \begin{bmatrix} \widehat{p}_{x_{k+1}}^{(i)-}  \\ \widehat{p}_{u_{k+1}}^{(i)-}\end{bmatrix} =  \begin{bmatrix}
  1 & \Delta t \\ 0 & 1
\end{bmatrix}  \begin{bmatrix} \widehat{p}_{x_{k}}^{i}  \\ \widehat{p}_{u_{k}}^{i}\end{bmatrix}$

$P_{k+1}^{-} = A_{k}P_{k}A_{k}^{T} + Q_{k}$
The intial values were taken to be:
$x_{o} = \begin{bmatrix} random()\\ 0 \end{bmatrix}$, $P_{o} = \begin{bmatrix}
  1 & 0 \\ 0 &1
\end{bmatrix}$
## References:
[1] [Welch, G. and Bishop, G., 1995. An introduction to the Kalman filter](https://perso.crans.org/club-krobot/doc/kalman.pdf).
