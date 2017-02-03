# Udacity-CarND-Advanced-Lane-Finding

# About

This project is part of Udacity's Self-Driven Car Nanodegree Program. The aim is to develop a pipeline through which evaluates video stream from the cameras set up in front of the car and output the lane lines, radius of curvature and position of the car respect to the center.

# Pipeline

Calibration matrix and distortion coefficients are calculated using calibration images provided by udacity. 

The steps via which an image goes through :-

1) Undistorted image is obtained using calibration matrix and distortion coeffients from above.

2) Perspective Transform is applied to get the bird's eye view of the lanes.

3) Different color thresholds are applied on the bird's eye view image to get binary image of the lanes.

4) Polynomial equations of left and right lanes are obtained in this step.

5) The line equations from above step are used to draw a polygon representing the lane boundary on which the car should drive.

6) The detected polygon boundary is warped on the input image.

7) Lane boundaries, Radius of curvature and position of the car with respect to center are displayed on the original image.


# Camera Calibration
