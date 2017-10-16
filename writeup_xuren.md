# **Finding Lane Lines on the Road** 

## @Author: Xu Ren
## @Date: 2017-10-14



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

My pipeline consisted of 5 steps. 

1. First, I convert the image to grayscale.
2. The image is then blurred.
3. Edges are then discovered by applying the Canny edge detection algorithm. 
4. A masked region is then created by selecting just an area of interest using vertices. 
5. Hough lines are then detected by applying the hough transformation and the final lines are drawn unto the original image. 

In the first iteration, the lines detected included the lane lines but also some other high contrasting edges that were not lane lines. While easy for the human eye, the algorithm simply accepted these edges as well due to their fitting criteria and lines were ultimately drawn back unto the original image that are beyond just the lane markings. To address this, we had to improve our draw_lines function. To do this, we further limited the areas where we would draw the lines by limiting the maximum areas for Y-axis and averaging the slopes and intercepts of the various lines. Furthermore, we apply some conditional logical to make sure that the current slope being evaluated is actually within a threshold of "steepness" such that it is plausible that the lines could be considered as lane lines. 


### 2. Identify potential shortcomings with your current pipeline


The biggest shortcoming I foresee is the problem of curvature. If the road is highly winding, the lines I have detected using linear slopes and intercepts may not be able to detect the curved lane lines. 

Another problem is when there are parallel objects traveling in the "viewport" of the car on either side of the lanes that may have contasting edges that resemble those of the lane lines but actually are not lane lines. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to do more pre-processing in order to pre-remove some of the objects that could be detected as lane lines later. 

Another potential improvement could be to to remove surrounding shadows or apply conditional color gradient logic that makes only the closest contrasting pixels most likely to be considered as lane lines rather than all highly contrasting gradients of colors. 
