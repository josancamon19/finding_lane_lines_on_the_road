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
[image2]: ./examples/image_with_lines.png "Image with lines"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.:

* I converted the images to grayscale.
* Then, manually using cv2.GaussianBlur, I removed the noise using a kernel_size of (5,5)
* Then I applied the cv2.Canny filter in order to get the edges between a certain threshold, in this case (50,150)
* Then I select the region of interest creating a mask and using cv2.fillPolly.
* Then I select some lines based on the arguments passed to cv2.HoughLinesP
* Then I drew the lines of lines found with cv2.HoughLinesP
* Finally I merged the red lines drew with the rest of the image black (0,0,0) with the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

* First, I found the slope in each set of lines.
* Then, I split the lines of each segment of the road (left lines, right lines)
* Then, I calculated x coordinates using y = mx + b and m = (y2-y1)/ (x2-x1)
* Finally, I drew the lines.

![alt text][image1]

![alt text][image2]


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the region detects as in the challenge video the divider is too near to the 
lane lines and there is a shadow at the other side, so in both cases it caused a lot of interference.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to using a different approach like find a way to deal with very curved scenarios, also trying to detect 
a larger portion of the landmark without interference with cars or other objects. 
