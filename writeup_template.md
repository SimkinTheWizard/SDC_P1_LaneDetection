# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.png "Grayscale"
[image2]: ./examples/blurred.png "Blurring"
[image3]: ./examples/edges.png "Edges"
[image4]: ./examples/roi_original.png "ROI - Original Image"
[image5]: ./examples/roi_edges.png "ROI - Edges"
[image6]: ./examples/hough_transform.png "Hough Transform"
[image7]: ./examples/lane_lines.png "Lane Lines"
[image8]: ./examples/draw_lines.png "Draw Lines Modification"
[image9]: ./examples/draw_lines2.png "Final Lane Lines"

---

### Reflection

### 1. Description of pipeline

The detection algorithm consists of several step beginning from the original image to the drawing lane lines on the image. The steps are as follows:

* __Converting the image to grayscale__

  First step of the pipeline is to convert the image to grayscale so that the edge information can be attained. [image1] Shows the result of conversion to grayscale.
  
  ![image1]
* __Getting rid of glithces on the edges by blurring the image__

  The image is filtered before calculating the gradients in order to remove small glitches. To do this operation I used a kernel of size 5x5. [image2] Shows the result of this operation.
  
  ![image2]
* __Edge detection and thresholding with Canny edge detector__

  The third step is to find the edges. A Canny edge detector is used for this operation. Lower threshold value is selected 50, and higher threshold is 130 for this operation. [image3] demonstrates the result of Canny edge detection.
  
  ![image3]
* __Masking the region or interest__
  As the fourth step of the pipeline the edges in the regions that cannot belog to lane lines are eliminated.
  [image5]
* __Finding the lane lines using Hough transform__




Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
