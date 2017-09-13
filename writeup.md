# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[blurred_image]: ./imgs/blurred_image.jpg "Blurred image"
[edges_image]: ./imgs/edges_image.jpg "Edges image"
[masked_image]: ./imgs/masked_image.jpg "Masked image"
[lane_lines_img]: ./imgs/lane_lines_img.jpg "lane lines image"
[final_output]: ./imgs/final_output.jpg "final image"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps.

1. First, I converted the images to grayscale, and apply a Gaussian filter to blur the picture:

![alt text][blurred_image]

2. Then, I found edges(or points with a large gradient) using canny filter:

![alt text][edges_image]

3. Later, I filter the image looking for a region of interest:

![alt text][masked_image]

4. Now, I use Hough transformation to look for lines on the image.

5. Ones I have a set of lines, I filter all lines looking for candidates for the left lane line and the right lane line. I do this filtering using thresholds for the slope of the line and intersection with the x axis.

![alt text][lane_lines_img]

6. Finally, I combine original image and lane line image.

![alt text][final_output]

### 2. Identify potential shortcomings with your current pipeline

There are several potential issues with my current implementation.

1. The region of interest depends on a hard coded pixels location, they are tuned from car to car, and they can become useless in case of a sudden change of position, for instance after a small accident.

2. Edges and line detection can fail if the color change in the image is not large enough, this can happen with old printed lines, overnight, or if the street is old and sections of the lines are missing.

3. Another issue occurs while driving on a curve. Candidates for lane lines are based on a slope threshold. It means that line segment at the end of the curve is going to have a larger slope regarding magnitude and slope could be outside the thresholds.


### 3. Suggest possible improvements to your pipeline

There are several possible improvements:

1. Transforming the image to a representation based on color saturation we could improve the resolution of yellow and white colors.

2. Lane lines don't change direction abruptly, so we could merge current image in the video with previous images to give hints to the algorithm about the most likely position of the lane lines.

3. Lane lines are well defined in the lower section of the image(closer to the camera), and it changes slowly. We could use a moving window starting from the bottom, find candidate lane lines in each window using lines in the window and the candidate lane line of the previous window and extrapolate the candidates to have the final lane lines. (This improvement is not that hard, but I don't have enough time to implemented, maybe later). 
