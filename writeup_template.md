# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

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

My pipeline consists of the following 5 steps:

1.  Convert the image to a grayscale image
2.  Perform the gaussian blur and canny edge detection on the grayscale image to trace out all of the edges 
3.  Create a 4 sided polygon mask for the image that defines the area where the lane detection algorithm will run 
4.  Perform the Hough transform in the masked area of the image where the edges have already been traced out to detect all of the straight lines that are contained within that area 
5.  Draw the detected lines (meeting certain criteria - see below) on a blank image and then recombine it with the original image to show the lane lines

In order to draw a single line on the left and right lanes, I modified the draw_lines() function in the following ways:

A.  (Grouping lines according to their gradient level) - I grouped lines according to their gradient level and placed them into two buckets: lines that resemble the left lane and lines that resemble the right lane
B.	(Find most dominant path) - I created a recursive function to detect the most dominant (or longest) path for both the right lane and the left lane.  Using the 2 separate line tables I created above, my code iterates through each line to find the longest path that it could create (meeting prescribed gradient and distance criteria).  The most dominant path is tracked during the recursive process and returned at the end 
C.	(Extrapolation) - Once the most dominant paths for both the right lane and left lane are known, I extrapolate them into one single line for each lane by first computing a single line that provides the best fit on all of the coordinates of the dominant path, and then run the line through a smoothing function that tracks the running mean of the start and end coordinates of the previous best fit lines.  The end result is one single line to mark each lane that transitions smoothly from frame to frame

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
