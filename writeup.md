# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.
 1. Convert the images to grayscale
 2. Smoothing / blurring the image
 3. Detect the eadge using Cany method call
 4. Apply image mask with static vertices to get the region of interest.
 5. Apply Hough transform on the masked edges to get the hough line and draw the line iterating over the output lines on top of the blank image of the same size as original. We also draw the line on top of original image to show the detected lines.

At the end of the code we ran the same pipeline on the couple of videos solidWhiteRight.mp4 and solidYellowLeft.mp4

On the step 5 above, in order to draw a single line on the left and right lanes, I careated clone of draw_lines function and given a name draw_solid_lines to keep the original draw line as it is.

For drawing the solid lines, I slightly deviated from the instruction provided to identify the left and right lanes. I used just the normal comparision method to separate part of the left lane and right lane. First, I initialized the x-axis and y-axis to a value which is out of image area, so we can populate the right value later with comparision. I also assumed the x-axis of left boundary and right boundary by values on xl_boundary and yr_boundary. I use this predefined value to compare with rest of the axises from lines variable to separte them left and right lanes. With this separaton, I am comparing each value to find the max and min points to draw line on left lane and right lane. I could also have stored each points x and y axis in a list but since we don't care about individual points for this project, I didn't do that

At the end of draw solid line, I calclate the x axis value of the buttom left and right lane as we want to start to draw from the buttom of the image. The buttom of the image value always have y axis's value 540 as that is our size of the image.

If you'd like to include images to show how the pipeline works, here is how to include an image:

[//]: # (Image References)

![alt text][image1]: ./test_image_output/redlane.png

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lanes are curve. Currently, it is assumed that all lanes are straight.

Another shortcoming is it is assumed that a specified zone is the area of interest for the lane.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to make the area of interest to find the lane a dynamic variable by identifying the possible lane location.

Another potential improvement is when we draw the lane, we need to draw it using the interest points not just by taking the max points and min point of x and y axises on left and right lane. 
