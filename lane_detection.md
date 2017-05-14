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

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

The project makes heavy use of skeletion code provided in 'Finding lane lines'.

### 1. Step-by-step pipeline implementation
1. Read input image
2. Convert image to grayscale. Converting images to grayscale helps lowering the complexity associated with dealing color images. With respect to the goal of this project, color related information may not be vital for detecting edges on road
3. Applying Gaussian blur to reduce the image noise and smoothen the image.
4. Apply Canny Edge detection to the output of Gaussian blur. This step will produce image consisting of edge which looks something like below. (INSERT IMAGE HERE)
5. Create a mask to extract areas which are of only intereset for finding edges.
6. Apply the region of interest mask to extract masked edges
7. Apply Hough transform to extract identiy lines of specific type from input image. For values of rho (distance) and theta (angular resolution), we started off with value of 1 for each of them and kept them tuning until we got expected results.
8. As intermediate step in Hough Transform, we extend the functionality from draw_lines() API.
![alt text][image1]


### 2. Potential shortcomings with your current approach

One potential shortcoming would be what would happen when ...

Another shortcoming could be ...

### 3. Possible improvements

A possible improvement would be to ...

Another potential improvement could be to ...