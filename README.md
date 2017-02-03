# Udacity-CarND-Advanced-Lane-Finding

# About

This project is part of Udacity's Self-Driven Car Nanodegree Program. The aim is to develop a pipeline through which evaluates video stream from the cameras set up in front of the car and output the lane lines, radius of curvature and position of the car respect to the center.

# Pipeline

Calibration matrix and distortion coefficients are calculated using calibration images provided by udacity. *cv2.findChessboardCorners()* and *cv2.calibrateCamera()* functions have been used for this purpose. 

The steps via which an image goes through :-

1) 
