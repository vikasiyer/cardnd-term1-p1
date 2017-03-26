
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on my work in this written report




---

### Reflection

Approach
At first I started the assignment leveraging the code used in the lessons to accomplish drawing red marker lines over white/yellow lane lines. After I got that working, I re-used the helper functions given in the Jupyter Notebook to get the solution.

### The Pipeline:

My pipeline consisted of 5 following steps:
1. Converted input image to grayscale.
2. Applied Gaussian Blur to the grayscale image.
3. Applied Canny Edge Detection to the output of bullet 2.
4. Defined a quadrilateral mask to filter out the area of interest from the rest. Applied the mask to the canny edge    
   detected image.
5. Applied Hough Transformation on the masked Canny Edge detected image. This would call the draw_lines() function to
   draw red lines on the lines detected by Hough Transform.



In order to draw a single line on the left and right lanes, I modified the draw_lines() function by doing the following:
1. Used the slope of the lines from Hough Transformation to determine if the line belonged to the left or the right
   lane. If the slope was negative or 0, I considered it to belong to the left lane. Else, it belonged to the right lane.
2. I introduced variables to keep track of the bottom most x,y point and the top most x,y point for both the lanes as I
   iterated through each line in the function.
3. After exiting the loop, I drew lines to join the bottom and the top points of both the lanes.


Here's an image that illustrates my pipeline:

[//]: # (Image References)
[image1]: ./test_images/Output/solidWhiteCurve.jpg "Solid White Curve"
[image2]: ./test_images/Output/solidWhiteRight.jpg "Solid White Right"
[image3]: ./test_images/Output/solidYellowCurve.jpg "Solid Yellow Curve"
[image4]: ./test_images/Output/solidYellowCurve2.jpg "Solid Yellow Curve 2"
[image5]: ./test_images/Output/solidWhiteCurve.jpg "Solid White Curve"
[image6]: ./test_images/Output/solidWhiteCurve.jpg "Solid White Curve"
![alt text][image2]
---

###2. Shortcomings with my current pipeline

Shortcomings:
1. The pipeline video output has flickering red lines.
2. The top edge of the red line tends to move in between the lanes occasionally for a few frames in the video.
3. The optional challenge output does not work so well.

I hope that the improvements mentioned below will address these shortcomings.



###3. Possible improvements to my pipeline

 Instead of only relying on the bottom and top most points to draw an extrapolated line, I am trying to calculate an average slope and average constant (b from y=mx+b) of all the lines in a lane. Once I get the average values, I will try to calculate the bottom and top points for both the lanes by assuming the "y co-ordinate" and calculating an "x-coordinate". I have already seen some improvements to the lane markers, though it does not work very well yet. Though the flickering has stopped for most part, the markers seem to meet at the top of the frame. I will work to correct this.
