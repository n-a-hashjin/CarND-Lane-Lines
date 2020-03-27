# **Finding Lane Lines on the Road** 

## Project Report

### Self-Driving Car Engineer Course


---

**Finding Lane Lines on the Road**

The goals of this project are the following:
* Make a pipeline that finds lane lines on the road
* Improving process through color detection
* Reflect on your work in a written report

The steps of this project can be presented as following:
* Reading video frame and converting it to grayscale
* Applying canny edge detection on the grayscale image
* Restricting lines detection area
* Applying hough transform to extract lines
* Averaging lines on each side to get one solid line for each side of road
* Improving process through color detection

[//]: # (Image References)

[image1]: ./writeup_images/lighting.jpg "detection using color filter under different lighting conditions"
[image2]: ./writeup_images/shadows.jpg "detection using color filter beside shadows"
[image3]: ./writeup_images/failed_to_detect.jpg "lighting conditions makes it difficult to detect lane lines"
[image4]: ./writeup_images/failed_to_detect1.jpg "shadows makes it difficult to detect lane lines"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the image to grayscale, then at the secondstep I used Gaussian filter to blur the image to reduce noise so the grayscale edge detection algorithm at the next step be able to extract edge image more accurate. I applied canny edge detection algorithm in the thirdstep.

The next step was applying hough transform to detect lienes of processed image from last step. In this step I tuned the parameters of edge detection algorithm.

In order to draw a single line on the left and right lanes, as last step, I modified the draw_lines() function by deviding detected lines to left and right side lines through differing them based on lines' slope. I used averaging slopes and y-intersections point's of lineson each sides to get a left and a right solid line and drawed it.
I put all above steps in a function named process_image() as my pipeline.

In order to complete challenge part, I improved above steps using a color filter. I got the Idea, when I diagnosed the raw output of previous pipeline and saw the shadows and highlights make it hard for this simple algorithm to detect correct lines. So I added a filter for a range of yellow and white colors in each frame before starting to process the image. I saw that the results significently improves but to make it more precise and durable I tuned again the parameters like hough transform parameters and thresholds. All this stepp in a new pipeline has been developed, i.e color_process(). At below see the result of using color filter to detect line as it goes through shadows and different lights.

![alt text][image1]

![alt text][image2]


### 2. Weaknesses of my current pipeline


The improved Algorithm although can detect lines even under presence of shadows and different lighting but rarely looses tracking of the lane line especially when there is strong changes in lighting and shadows. See the bellow images.
Below you can see where color filter failed to detect lines. It might can be improve with better parameter tuning.

![alt text][image3]

![alt text][image4]



### 3. Suggest possible improvements to your pipeline

A possible improvement would be applying markov chain based on last lines to predict next lines that can prevent losing the line track.

Another potential improvement could be updating color filters using adaptive algorithm, i.e. uper and lower limit of color range detection. These can increase the accuracy, reliability and robustness of system under inconsistent lighting conditions.

