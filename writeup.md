# Finding Lane Lines on the Road

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road

* Reflect on your work in a written report


[//]: # (Image References)

[grayscale]: ./pics/grayscale.png "Grayscale"
[canny]: ./pics/canny.png "Canny Edge Detection"
[rois]: ./pics/rois.png "ROIs"
[edges_rois]: ./pics/edges_rois.png "Canny Edges ROIs"
[houghlines]: ./pics/houghlines.png "Hough transform"
[houghlines]: ./pics/houghlines.png "Hough transform"
[lane]: ./pics/lane.png "Detected lane"

---

### Reflection

### 1. Description of the pipeline

My pipeline consisted of 5 steps.

First, I converted the original RGB image to grayscale.

![grayscale][grayscale]

Then I applied Gaussian smoothing to reduce the noise. The output of this step I fed to the Canny edge detection algorithm. This gave me all edges in the image.

![canny][canny]

Afterwards I filtered out two regions of interest, one for the left lane line and one for the right one.

![rois][rois]

The edges in those regions most probably belong to the lane lines.

![edges_rois][edges_rois]

In the next step, I applied Hough transform on the edges found in the ROIs.

![houghlines][houghlines]

In order to draw two lines (matching the left and right lane line, respectively) into the image, I wrote a new function `draw_lines2()`. In this function I calculated the angles of the Hough lines in the regions of interest. Then I calculated the median and the standard deviation of the angles all the lines in each ROI. The lines with angles which are more than 1 standard deviation away from the median I dropped. With the remaining lines I did a line fit and draw the resulting line for each ROI in the original image. The result is depicted below.

![lane][lane]

### 2. Shortcomings of the Pipeline

The construction of the pipeline works only well, as long as the majority of the Hough lines belong indeed to the lane lines. If there are too many outliers the median of the angles would not be appropriate.

Also, the pipeline is not good in detecting lane lines when the contrast to the street is low.

### 3. Possible Improvements

To overcome the above mentioned shortcomings, I would suggest filtering out all lines where the angle is not in a certain range (e.g. 50°-70° and 110°-130° for the left and right lane line respectively).

Another improvement could be, to increase the contrast and fine tune the parameters of the pipeline in order to detect lane lines in low contrast areas.
