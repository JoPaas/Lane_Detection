# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./mask_canny.jpg "Mask / Canny"
[image2]: ./test_images_output/whiteCarLaneSwitch.jpg "Lane Lines"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First I converted the image to HSV scale to better be able to pick colors. I applied a mask each for white and yellow areas, using the HSV parameters to also concider e.g. dark/dirty white. The combination of the two is the baseline for edge detection. 

The edge detection was carried out using canny and higher upper and lower thresholds than in a grey scale image, because the edges are black to white instead of different tones of grey. after that a mask as the region of interest of the road was applied. The images show the binary mask and the edges inside the region of interest.

![alt text][image1]

Finally I applied the Hough transform and split right and left lane line. A two-sigma rule was used to throw out any line which slope wasn't in the 95% area of the total distribution. Then I used the line start and end points to fit a poly line of first degree.

![alt text][image2]


### 2. Identify potential shortcomings with your current pipeline


The pipeline would not be able to detect lane lines with a large curvature. The challenge video still works but for greater curvatures the polyfit would have to have a higher degree and also the hough transform would fail.
Also the pipeline only detects one line per side, so it would get confused if there are several lines on one side of the ROI, which is split in the middle.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be adding a filter or estimator on the lane line position, so the line is detected smoother.

also further assumptions like lane width could be taken into account to improve the region of interest. On the other hand the algorithm could be improved so a region is not needed anymore and lines in the whole picture can be detected. Then of course there has to be a way of differentiating between different lane lines.