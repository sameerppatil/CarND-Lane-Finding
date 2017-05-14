# Project 1 writeup: Finding Lane Lines on the Road

---
**Project Objective**
* In this project, we aim to find lane lines from images and videos
* We define a pipeline using sample images and extend that functionality towards videos

**Document objective**
In this document, we address discuss about aspects of project design considered during implementation.
* How the pipeline is implemented?
* What aspects of input data influence design decision?
* In what scenarios, the pipeline would fall short of accurately finding lane lines.

[//]: # (Image References)

[image1]: ./examples/my_grayscale.jpg "Grayscale"
[image2]: ./examples/my_canny.jpg "Canny Edges"
[image3]: ./examples/my_lines.jpg "Lane lines"

---

### Reflection

The project makes heavy use of skeleton code provided in 'Finding lane lines'.

### 1. Step-by-step pipeline implementation
1. Read input image
2. Convert image to gray-scale. Converting images to gray-scale helps lowering the complexity associated with dealing color images. With respect to the goal of this project, color related information may not be vital for detecting edges on road
![Grayscale image][image1]

3. Applying Gaussian blur to reduce the image noise and smoothen the image.
4. Apply Canny Edge detection to the output of Gaussian blur. This step will produce image consisting of edge which looks something like below.
![Canny edges output][image2]

5. Create a mask to extract areas which are of only interest for finding edges.
6. Apply the region of interest mask to extract masked edges
7. Apply Hough transform to extract lines of specific type from input image. For values of rho (distance) and theta (angular resolution), we started off with value of 1 for each of them and kept them tuning until we got expected results.
8. As intermediate step in Hough Transform, we extend the functionality from draw_lines() API.

##### draw_lines()
- In this function, we are given an array of lines where each of the line a tuple of four points in coordinate system.
- Our goal is to connect this dotted lines so that one continuous line can be plotted
- Using these coordinates, we calculate the slope, intercept, length for each line.
- Based on if the slope is positive or negative, we determine if the line is left line or right line. A left line will have positive slope while right line will have negative slope.
- For each iteration, we keep track of minimum value of y which will be one of the point out of two for whole line.
- Once slopes and intercepts for all lines are calculated, for each side (left and right), we calculate average slope and intercept using the length as one of the weight.
- Now, using y (max and min), avg. slope, and avg. intercept, we find two values of x'es. Now, using this combination of x1, y1, and x2, y2, we plot continues lines and extend the lines calculated by Hough Transform.
![Extrapolated lane lines][image3]


### 2. Potential shortcomings with your current approach

One potential shortcoming would be what would happen when ...

Another shortcoming could be ...

### 3. Possible improvements

A possible improvement would be to ...

Another potential improvement could be to ...