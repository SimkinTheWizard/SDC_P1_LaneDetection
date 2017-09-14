# SDC_P1_LaneDetection

# **Finding Lane Lines on the Road** 

---
Implementation and results are in the [Jupyter notebook](./P1.ipynb).

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
[image6]: ./examples/hough_transform.png.png "Hough Transform"
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
  As the fourth step of the pipeline the edges in the regions that cannot belog to lane lines are eliminated. I used a region of interest in the images that can be lanes. [image4] shows the region of interes selected in the image.
  
  ![image4]
  Applying this region of interest to edge image results in the edges shown in [image5].

  ![image5] 
* __Finding the lane lines using Hough transform__
  After finding lane lines I employed Hough transform on the edge image to find the lines. I picked the line thickness as 3 points and angle as 2 degrees. I picked the decision threshold to 100 points. Since the dashed lines have a large gap between consecutive lines, I used a large value (100) for *max_line_gap* parameter. And I used a small value for *min_line_len* parameter. [image6] shows the result of the lines found with Hough transform.
  
  ![image6] 
  
* __Combining the lines with the image__
  Finally, I combined the lane image with the original image as shown in [image7].
  
  ![image7] 

## 1.a. Modificatons to *draw_line()* function
   I modified the *draw_line()* function in order to extend the lines to the limits of the region of interest (ROI). For each line that would be drawn I fit a line, which is denoted by `y=m*x+n`. For this specific case where final y values are known, I fit a line `x=y*m+n`. And found the `m` and `n` values from the x and y values of the lines. After that I extended the lines to the edge y values of the ROI. [image8] shows the extended lines, and [image9] shows the lines overlaid on the original image.
   
  ![image8]
  
  ![image9] 
  
  Another change I made in the function is for the challenge video. In the challenge video there are a lot of shadows and sudden changes on tarmac. To ignore these changes I put a limit to the angles of the lines that will be drawn. I did this by fitting a second line `y=m*x+n` to the x and y values and discarded the values that fell in a certain range.
  
  
### 2. Potential shortcomings with the current pipeline

The obvious shortcoming of the current pipeline is that when there is curvature on the road. The reason for this is that we are searching for lines with Hough transform. 

Another shortcoming is that shadows could be misinterpreted as lane lines on the road if the sun is bright enough. Also long vehicles can be interpreted easily lanes since they will have a large edge. 


### 3. Possible improvements to the pipeline

A possible improvement to the pipeline might be to separate the ROI into two parts in y-axis. With two ROI parts a better line fitting can be found. In addition to that, this solution would help us to estimate the curvature of the road. Another solution would be to use a circular Hough transform instead of a linear one. The resulting circle could be fit a second order polynomal, instead of first order.

I also neglected color information on the image, which is a very useful information. We know that lane lines are either white or yellow. Color filtering can be implemented to enhance the result and eliminate a lot of false positives.

Finally there is some shape information we did not employ here. We all know that lane lines are within a certain thickness range. This thickness information can be used too. Lines found with the Hough transform can be grouped together based on their distances in the x-dimension. With this grouping we can find the thicknesses of detected lines, and accept/reject some of them according to this criteria. 

