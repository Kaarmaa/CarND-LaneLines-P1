# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.


My pipeline consisted of 6 steps. 
	- Gray the image
	- Blur the image
	- Use Canny edge detection to extract edge data
	- Mask the Canny processed image to only use the edges in the defined region where the road markings exist
	- Use the Hough transform to further process the extracted edges
		- Filtered on slope angle to remove vertical and horizontal lines
		- Filtered on length of lines to eliminate very small edges
	- Combine all lines that represent road markings of interest, fit a curve for each left and right side of lane, overlay on image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
	- Storing all points of extracted edges, filtered by Left and Right of lane 
	- Performing a line fit for each left and right separately 
	- Using the vertical min/max of the selected region and drawing the line from the fit from min to max

If you'd like to include images to show how the pipeline works, here is how to include an image: 


### 2. Identify potential shortcomings with your current pipeline

1) Long edges that are not the lane markings can skew the line fit greatly (Bridge crossings for example)
2) I am only using a single straight line from min to max of vertical masked region. This does not deal with curves very well.


### 3. Suggest possible improvements to your pipeline

To compensate for 2.1, I have already filtered the possible slopes of the hough lines to a narrower span, but it could be tightened up
To compensate for 2.2, The single lines representing lane limits could be subdivided in the vertical space to allow better for curvature
