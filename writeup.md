# **Finding Lane Lines on the Road** 

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

My pipline is the following:
1. Making a copy of the original image to use it later to visualize the results
2. Converting the image to grayscaled
3. Using a gaussian_blur with kernel_size of 3
4. Filtering for the hell pixels to get rid of noise and to focus on lanes boundaries
5. Application of canny edge detector
6. Cutting out a rectangle shaped region of interest
7. Using hough line detection
8. Cut out line to visualize them only in the region of interest
9. Putting lines on the original image

Modification of draw_lines:
In order to build solid line from the line segments:
1. Calculation of the slope of each segments
2. Calculation of a mid value of slopes which is on the half-way between this smallest and greatest slope, it will be used as a treshold
3. Split the line segments into two parts based on their slope and the calculated slope mid value
4. Generation of line from the line segments by fitting them to a polynomial of 1 degree
5. Calculation the points on the line on the edges of the image => later on they will be only visualized in the region of interest

### 2. Identify potential shortcomings with your current pipeline

- If one of the two lane boundaries is not visible on the picture or their slope is too similar then the way how the lines are seperated is producing an incorrect output
- The currently used parameters are not proper to be used in case of limited visibility (darkness, rain etc.)
- The region of interest could change up to the position of the camera

### 3. Suggest possible improvements to your pipeline

- Some parameters (like limit in point 4) could be tuned automatically based on the average value of all pixel, so that it could adapt to different light conditions
- In video mode "jumps" of line could be filtered by comparing the line position to the position on the previous frame
- After splitting the segments into two sets, a post filtering based on their position would be useful the filter out classification errors and noise
