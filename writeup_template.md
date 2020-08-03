# **Finding Lane Lines on the Road** 

## by Asil Kaan Bozcuoglu


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Description of my pipeline. 

My initial pipeline (the one that does not successfully process the challenge video) consists of 5 stages. 
First, I convert the images to grayscale, then I filter the grayscale image using Gaussian blur. 
Next, I apply Canny edge detection algorithm to detect edges. After that, I mask out the unrelevant 
zones of the image which do not correspond to the road. Finally, I transform the image to Hough space

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
a) identifying which lines belong to the left lane  which lines belong to the right lane by
looking at their slopes and their location. If their slopes and locations are not within the expected
limits, I count them as outliers and filter them out.

b) For the left lane lines and the right lane lines, I apply linear regression to get a single 
average line for each.

c) if the slope of one of the average lines is not within the expected
limits, I just take the average slope and interceptation.

d) draw the average line of each lane at the below half of the image

Later on, I improved my pipeline for the challenge video:
First, I apply a yellow-white filter to the image for being less sensible to avoid hallucinating lanes inside trees and highway direction separator 
Then, I convert the images to grayscale. 
In order to survive from shadows and asphalt color changes, I am using otsu thresholding instead of Gaussian blurring. 
The rest is same with the first version

### 2. Identify potential shortcomings with your current pipeline

a) If sterring angle is great (like in u turns), the slope assumptions could be not valid.
b) if we have a white vehicle in front of us, we would have too much noise. I believe the pipeline will be messed up
c) Many different asphalt colors and shadowings can even hurt my improved pipeline
d) During nights, headlights can create different lighting conditions and shadows.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to implement an automatic on-the-flight camera calibration

Another potential improvement could be to feed the pipeline with previous frame's lanes to have an expectation.

Finally, we can employ a vehicle detection algorithm to filter the vehicles out of the camera images. This can solve the shortcoming (b).
