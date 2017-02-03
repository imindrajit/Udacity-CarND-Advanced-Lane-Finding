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

OpenCV functions *findChessboardCorners()* and *drawChessboardCorners()* have been used to calibrate the camera using chessboard images provided by udacity. The distortion coefficients and camera calibration matrix obtained here are used in the pipeline for undistorting images.


# Step 1 ( Undistort Images )

The camera calibration matrix and distortion coefficients obtained from above are used for undistorting the images. This code is present in cell no. 9 of advanced_lane_finding.ipynb.

Original Image             |  Undistorted Image
:-------------------------:|:-------------------------:
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/undistorted_images/straight_lines1/original.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/undistorted_images/straight_lines1/undist.jpg)

If you observe closely, the edges of the image are a bit different so, the distortion effects have been removed.


# Step 2 ( Bird's Eye View )

Perspective transform is applied on the undistorted from above step. This code is present in cell no. 10 of advanced_lane_finding.ipynb. In normal view the lanes can be seen as converging together but to get the exact lanes for the car to drive we need parallel structure of the lines. For this purpose it is important we do perspective transform. This also helps in only focussing on the lane part of the image. 4 source points from the original image are picked and also 4 destination points, which form a rectangle, are selected. *cv2.getPerspectiveTransform()* is used to get the transformation matrix. *cv2.warpPerspective()* is used to get the warped image.

Original Image             |  Bird's eye view of Image
:-------------------------:|:-------------------------:
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/birds_eye_view_images/straight_lines1/original.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/birds_eye_view_images/straight_lines1/birds_eye.jpg)

