# Writeup: Sensor fusion and object detection (Part 2)
## 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?

### Filter
In the filter step, the prediction from the last measurement must be calculated. This prediction must be compared to the next measurement and the track must be updated. The prediction step follows the formula in the following image. The matrix F is the state transformation matrix and transforms data points from sensor space to measurement space. To caluclate the estimation error covariance matrix P, the process noise covariance Q is needed. The Q in the exercises is only a 2x2 matrix, however Q must be a 6x6 matrix for this project. 

To update the track, the residual, gamma must be calculated. The gamma compares the new measurement, z with the state estimation. The gamma is used to calculate the updated x value along with the Kalman gain K and the covariance S.

The most difficult part of this section for me was undersanding the difference between h(x) and H. I was aware that H should only be used for linear equasions such as lidar, however, there is logic in both get_hx and get_H to return different matrices for differing sensor types. Eventually I was able to figure out that hx replaces the dot product calculation H * x to find gamma. 

So for linear lidar: z(3x1) - (H(3x3) * x(3x1))(3x1)

and for non-linear camera: z(3x1) - f(x)(3x1)

![Predict and Update](images/kalman_1d_equations.png)

Predict and Update

## 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 


## 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?


## 4. Can you think of ways to improve your tracking results in the future?