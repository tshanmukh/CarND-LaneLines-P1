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

I have divided the problem into smaller problems as explained in the classroom.
1. First I have created a function named mark_lanes which accepts input as an image file or an numpy array of the image data
2. Converted the image to grayscale image
3. Used the gaussian filter on the gray image to remove the noise
4. Used the canny edge detector which uses the gradient method to detect the edges
5. Passed the above image to the Hough transform where I performed the lines extraction by varying all the hough parameters and selected certain values which gave the best result
6. I have modified the *draw_lines()* so that it will draw a one straight line extrapolated over the existing lines. I calculated the slopes and intercept values for the lines obtained
7. Then calculated the maxslope line and minslope lines over left and right portions and obtained the new lines and drew them using cv2.line funtion

![FinalOutput]("test_images_output/solidYellowCurve2.jpg")


### 2. Identify potential shortcomings with your current pipeline


1. one potential short come is we are using straight line to detect the lane this can be a major issue as we can encounter sharp turns 
2. If there is a vehicle close ahead causing obstruction to the lanes
3. During the dark when the street lights are lit there is lot of noise in the each frame as the color of lights and the lane markings may be the same 
4. *we are parsing the whole image data each time in a video clip this takes lot of cpu time and reduces the efficiency*
### 3. Suggest possible improvements to your pipeline

1. We should be using complex curves of higher order than 2 which can be produced by the np.poly funtion to detect the lane markings
2. We need an alternate to obtain the postion of car when the lane markings are blocked by cars ahead or some external things
3. We can use different color levels like the blue, green and red simultaniously and identify which of this could give best lane markings or add the lane markings obtained in each color level so we can identify lanes in the dark
4. we can obtain the difference part in the two adjacent frames and use this information to obtain the lane markings in the next frame so we correlate the data inbetween the frames
