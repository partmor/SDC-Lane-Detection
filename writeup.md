# **Finding Lane Lines on the Road** 

[//]: # (Image References)
[image1]: ./examples/grayscale.jpg
[original]: ./test_images/solidYellowCurve.jpg
[adjusted_gamma]: ./test_images/adjuste_gamma.jpg
[canny]: ./test_images/canny.jpg
[roi]: ./test_images/roi.jpg
[hough]: ./test_images/hough.jpg
[extrapolated_on_image]: ./test_images/extrapolated_on_image.jpg

### 1. Pipeline description

Convert the image to grayscale, apply a Gaussian noise kernel, and the Canny edge detection algorithm, using a 3:1 threshold ratio:
![canny]
Define a trapezoidal ROI to focus on the area of the image where the lanes are:
![roi]
Apply the Hough transform to the ROI-bounded detected edges, retrieving the detected segments.
![hough]
In order to draw a single for each lane, a second implementation for the `draw_lines()` function was created:  `draw_lines_extrapolated()`. In this function a certain Hough line is tagged as belonging to the left/right lane by checking the sign of its slope. Two additional checks are also performed, in order to avoid high leverage outliers:
+ Horizontal position of the line midpoint with respect to the ROI's top edge midpoint.
+ Slope is in a reasonable range (here 45º +- 20º).

After tagging the lines, a linear least squares fit is performed for each lane: collecting the coordinates of the Hough lines endpoints and regressing *x* against *y*:
![extrapolated_on_image]


### 2. Potential shortcomings


...


### 3. Possible improvements

...