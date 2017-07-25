# **Project 1 -- Finding Lane Lines on the Road**



---

### Finding Lane Lines on the Road

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Implementation
1. Pipelines
  * Load image
  * Apply grayscale()
  * Apply gaussian_blur()
    - Kernel size = 5
  * Apply canny()
  * Apply region_of_interest()
    - (120,imshape[0]),(470, 300), (490, 300), (imshape[1] x 0.90, imshape[0])
  * Apply hough_lines()
    - Apply draw_lines()
    - rho = 1 # distance resolution in pixels of the Hough grid
    -  theta = np.pi/180 # angular resolution in radians of the Hough grid
    -  threshold = 25     # minimum number of votes (intersections in Hough grid cell)
    -  min_line_length = 45 #minimum number of pixels making up a line
    -  max_line_gap = 15    # maximum gap in pixels between connectable line segments

My pipeline consisted of 6 steps listed above. The corresponding parameters are also listed.

2. Enhancements of draw_lines() function
  * Slope-based filtering
    - to get rid of the horizontal noisy line segments
    - to distinguish between right and left lane line
  * Extrapolated the points along the lane to form solid lines
  * Update the points in current frame using a weighted sum of points coordinates in current frame and previous frame, i.e. current_frame = 0.7 x current_frame + 0.3 x previous_frame


The end result looks like this:

[![SolidWhiteRight](https://img.youtube.com/vi/o4kOLKmLCTs/0.jpg)](https://www.youtube.com/watch?v=o4kOLKmLCTs "SolidWhiteRight")

[![SolidYellowLeft](https://img.youtube.com/vi/PHPn1BR9mfQ/0.jpg)](https://www.youtube.com/watch?v=PHPn1BR9mfQ "SolidYellowLeft")




### 2. Identify potential shortcomings with your current pipeline

  * The canny edge thresholds may be too tight, resulting no edge points (at the right lane line) being detected in some frames. A logic is added to the code to detect this case and uses previous frame results instead


### 3. Suggest possible improvements to your pipeline

  * While I am only using a weighted sum of previous frame and current frame. More frames can be averaged to calculate the lines at current frame.
