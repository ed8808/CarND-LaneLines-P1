## Self-Driving Car Engineer Nanodegree
# Project 1: Finding Lane Lines on the Road

Images from car camera are firstly converted to gray scale for Canny edge detection
Original -> Grayscale -> Gaussian blur -> Canny Edge detection

Then the region of interest, or ROI is formed from 4 vertices like a trapezium.

The Hough transformation is used to extract straight lines within ROI in Catesian plane by searching for curve intercepts in Hough plane
Red lines are finally overlayed on lane lines 

### How to optimize the detection algorithm?
  1.  The Gaussian blur kernel matrix: 
      - Kernel size: The larger the kernel size, the more the blur.  
      - Too large kernel size can result in loss of details.
  2.  Canny edge detection low and high threshold:
      - If grayscaled pixel > high threshold
          pixel = 255
      -  Else if grayscaled pixel < low threshold
          pixel = 0
      -  Else 
          if pixel is connected to valid edge
            pixel = 255
          else
            pixel = 0
      - Low, High = 100, 200 are used
       
  3.  ROI
      - Select region just enough to cover the lanes
      
  4.  Hough transform
      - threshold:
        - the thicker the line, the more the intercepts and higher threshold
      - Progressive Probabilistic Hough Transform
        - minLineLength: Minimum length of line. Line segments shorter than this are rejected.
        - maxLineGap: Maximum allowed gap between line segments to treat them as single line.
       - threshold, minLineLength, maxLineGap = 50, 100, 150 are used
       
  5.  Draw the final overlay red lanes
        - differentiate left and right lanes by sign of slope
        - save slope and points separately from sides
        - calculate mean of slope m, then mean of y-intercept c from equation c = y - mx where y and x are points from Hough
        - lane lines top and bottom y values are defined as 60% and 100% of image height
        - lane lines top and bottom x values are calculated from x = ( y - c ) / m
        - lane lines are formed from 2 points on each side
        
## Optional challenge:
1. video dimension is 1280 x 720 instead of 960 x 540, need generic codes to support both
2.  line lane is not straight but bending in turns
3.  other white objects on road such as cars can be falsely regarded as lane lines
4.  solution: instead of using a single trapezium with 4 vertices for ROI, new ROI consists of 2 trapeziums each just barely covers each lane
    
    
     

