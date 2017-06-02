# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

Goals:
* Make a pipeline that finds lane lines on the road
* Modify the code to draw segmented and full lane lines on images
* Modify the code to draw cuved lane lines on images

[//]: # (Image References)

[image1]: ./test_images_output/gray/gray_solidWhiteCurve.jpg "Grayscale"

[image2]: ./test_images_output/segmented/segmented_solidWhiteCurve.jpg "Pipeline"

[image3]: ./test_images_output/full/full_solidWhiteCurve.jpg "Full line"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline to find lane lines consists of 6 steps. (After reading in the image)
1. change the image to gray scale. As shown below.
2. Apply Gaussian Blur on the image, using kernel size of 5.
3. Apply Canny edge detector on the blurred image to get the gradient of pixels.
4. Bound the region of interest where the lane lines are.
5. Apply the hough transform and draw the detected lane lines on the image.
6. Add weight on the lines to the original image so the lines look more transparent.
Note: I modified the hough_lines() function to return both the lines and the image.

##### sample image
![alt text][image2]

To draw the full lines. I modified the draw_lines() function as follows:
1. Find the slopes of each lines
2. Seperate them into left and right according to their slope (greater than 0.4 or less than -0.4)
3. Average each the left and right lines
4. Compute the slope of each side
5. Compute the top and bottom point according to the slope
6. Draw the line

##### sample image on test image
![alt text][image3]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcomings with this current pipeline is that when the camera is not facing directly at the lane lines (lane lines are shifted to the right or left), the paramters need to be redefined, and it would fail if the driver is switching between lane lines etc.

Another shortcoming is when the gradient is not that strong, for example at night. Even though it is hard for human to see at night as wel, the current pipeline can be improved if we filters other than grayscale. 

### 3. Suggest possible improvements to your pipeline

As mentioned in the shortcoming, one of the improvement can be made is use filter for night vision so the computer can see the lane more clearly.

In general, I think this pipeline is good for pre-defined condition (when the lane lines is known to be directly in front). However, when the environment changed (car blocking the line etc), our algorithm won't detect the lane lines well. 
