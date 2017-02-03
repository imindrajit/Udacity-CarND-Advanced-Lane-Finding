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

OpenCV functions *findChessboardCorners()* and *drawChessboardCorners()* have been used to calibrate the camera using chessboard images provided by udacity. The distortion coefficients and camera calibration matrix obtained here are used in the pipeline for undistorting images. Code can be found in **cell no. 4** of advanced_lane_finding.ipynb.


# Step 1 ( Undistort Images )

The camera calibration matrix and distortion coefficients obtained from above are used for undistorting the images. This code is present in **cell no. 9** of advanced_lane_finding.ipynb.

Original Image             |  Undistorted Image
:-------------------------:|:-------------------------:
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/undistorted_images/straight_lines1/original.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/undistorted_images/straight_lines1/undist.jpg)

If you observe closely, the edges of the image are a bit different so, the distortion effects have been removed.


# Step 2 ( Bird's Eye View )

Perspective transform is applied on the undistorted from above step. This code is present in **cell no. 10** of advanced_lane_finding.ipynb. In normal view the lanes can be seen as converging together but to get the exact lanes for the car to drive we need parallel structure of the lines. For this purpose it is important we do perspective transform. This also helps in only focussing on the lane part of the image. 4 source points from the original image are picked and also 4 destination points, which form a rectangle, are selected. *cv2.getPerspectiveTransform()* is used to get the transformation matrix. *cv2.warpPerspective()* is used to get the warped image.

Original Image             |  Bird's eye view of Image
:-------------------------:|:-------------------------:
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/birds_eye_view_images/straight_lines1/original.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/birds_eye_view_images/straight_lines1/birds_eye.jpg)


# Step 3 ( Apply Color Thresholds )

Color thresoholding is applied on the bird's eye view image from above. This is done so that we can filter out only the lanes which are of interest to us, both yellow and white lane lines. The code can be found in **cell no. 12** of advanced_lane_finding.ipynb. We will aplly two different thresholdings for yellow and white color.

 i) ***Red Color Channel of RGB*** - We use *cv2.threshold()* and min_thresh = 220 and max_thresh = 255. Red channel does a great job of identifying the lane lines.
 
 ii) ***Yellow Thresh on HSV Color*** - HSV format is very good for color detection. So, we converted RGB image to HSV and then applied threshold ((10, 100, 100), (50, 255, 255)) to obtain yellow color patches.
 
 iii) ***White Thresh on HSV Color*** - Similarly, white color patches were found by using threshold ((50, 0, 180), (255, 100, 255)).
 
 iv) ***White Thresh on HLS Color*** - Some, white patches were missed due to different lighting conditions. So, we converted the image from RGB to HLS format and extract those missing white patches. Threshold range - ((0, 200, 200), (255, 255, 255)).
 
 v) ***White Thresh on RGB Color*** - We still found that some minute white colors from lanes were missing so, we extracted them from RGB image. Threshold range - ((220,220,220), (255,255,255))
 
 ***Combined Threshold*** - We use OR condition with all the above thresholding techniques and obtain the final binary image.
 
 Bird's Eye Image          |  Red Thresh               |   Yellow HSV
:-------------------------:|:-------------------------:|:
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/red_channel_thresh_images/straight_lines1/original.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/red_channel_thresh_images/straight_lines1/red_thresh.jpg) | 
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/yellow_hsv_thresh_images/straight_lines1/yellow_hsv.jpg)

 White HSV Thresh          |  White HLS Thresh
:-------------------------:|:-------------------------:
![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/white_hsv_thresh_images/straight_lines1/white_hsv.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/white_hls_thresh_images/straight_lines1/white_hls.jpg)  |  ![](https://github.com/imindrajit/Udacity-CarND-Advanced-Lane-Finding/blob/master/output_images/white_normal_thresh_images/straight_lines1/white_hls.jpg)


