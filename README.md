## Finding Lane Lines


[//]: # (Image References)
[image1]: ./test_images_output/origin.jpg "origin"
[image2]: ./test_images_output/gray.jpg "gray"
[image3]: ./test_images_output/blur.jpg "blur"
[image4]: ./test_images_output/edges.jpg "edges"
[image5]: ./test_images_output/roi.jpg "roi"
[image6]: ./test_images_output/lines.jpg "lines"
[image7]: ./test_images_output/result.jpg "result"


Overview
---
In this project, I will use the tools about computer vision to identify lane lines on the road. I will develop a pipeline on a series of individual images, and later apply the result to a video stream (really just a series of images).


The project
---
The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Improve this pipeline
* Reflect on my work


Ideas for Lane Detection Pipeline
---
Some OpenCV functions I have used for this project are:

cv2.inRange() for color selection  
cv2.fillPoly() for regions selection  
cv2.line() to draw lines on an image given endpoints  
cv2.addWeighted() to coadd / overlay two images cv2.cvtColor() to grayscale or change color cv2.imwrite() to output images to file  
cv2.bitwise_and() to apply a mask to an image  


Build a Lane Finding Pipeline
---
Using the following image as example, my pipeline consisted of 6 steps. 
![alt text][image1]

1. Converted the images to grayscale from RGB model 
![alt text][image2]  

2. Use cv2.GaussianBlur() to blur the image
![alt text][image3]  

3. The first core operation: detect edges of a gray model image
![alt text][image4]  

4. After the edges have been got, my next step is to define a region of interest(i.e., ROI), this method is old but efficient. Cause the camere installed on the car is fixed, so the lane lines is in a specific region, usually a trapezoid.
![alt text][image5]  

5. Anothe core operation: hough transform edges to a set of lines represent by start point and end point. Hough transform get the image of lane lines we want.
![alt text][image6]  

6. Finally, we add the lane lines image and innitial image together.
![alt text][image7]  


Test on videos
---
You know what's cooler than drawing lanes over images? Drawing lanes over video!

We can test our solution on two provided videos:

`solidWhiteRight.mp4`

`solidYellowLeft.mp4`  

The result is in [test_videos_output](https://github.com/Bhargav-Kumar98/Lane-Lines-Finding-Project/tree/main/test_videos_output): white.mp4 and yelloe.mp4.


Improved lane finding pipeline
---
At this point, I have the Hough line segments drawn onto the road, but what about identifying the full extent of the lane? Therefore I will improved my pipeline to do this. 

The first step is to diveded the detected lines into left set and right set.
Then in each line set, several special lines are choosen as basic to draw full line. 

The result is in [test_videos_output](https://github.com/Bhargav-Kumar98/Lane-Lines-Finding-Project/tree/main/test_videos_output): white_improved.mp4 and yellow_improved.mp4.
