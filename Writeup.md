[//]: # (Image References)

[image1]: ./examples/YW.gif "White Yellow Mask"
[image2]: ./examples/GR.gif "GrayScaled"
[image3]: ./examples/GB.gif "Gaussian Blur"
[image4]: ./examples/CED.gif "Canny Edge Detection"
[image5]: ./examples/ROI.gif "Region of Intrest Mask"
[image6]: ./examples/Lines.gif "Extrapolated Lines"
[image7]: ./examples/Final.gif "Lanes Detected"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:
First, I apply a HLS color filter, which enhances the colors yellow and white.  

![alt text][image1]

The advantage of using a HLS color filter over one in RGB is that it's easier to describe a
color range in HSV. While there is no need for this filter for the first to problems. This 
filter helps with the optional challenge. This approach was inspired from the approach by
[Naoki Shibuya](https://medium.com/towards-data-science/finding-lane-lines-on-the-road-30cf016a1165).  

Second, I grayscale this image we acquire from the color filter:

![alt text][image2]

Third, I added a gaussian smoothing on it to blur out any noise in the image due to imaging.

![alt text][image3]

While this step helps when there is no color filter. For the optional problem, where the 
color filter is used I don't think it has much effect since most noise is already cleared out.

Fourth step is Canny edge detection. I chose the minimum line length as 5 and max line gap as 10.

![alt text][image4]

Then we apply a region of intrest mask that selects the region where the lane lines are
most likely to be present. 

![alt text][image5]

The choice depends generally on camera placement, which is why 
two diffrent regions were selected for Normal Problems and the challenge problems. The region
is a trapazoidal shape.

The sixth and final step is to generate lines for lanes. This is done by averaging lines on 
this frame and then combining them with the average slopes from previous frame.

![alt text][image6]

While using just a wieghted average frame (wieghts bieng the length of the linesegments) works 
perfectly for still images. For videos this creates jitters in the line. For smoothening the 
line jitters in between frames, I combine the wieghted average with a combined average from 
all the previous frames.

After this I combine the lines back to generate the final stream.

![alt text][image7]

### 2. Identify potential shortcomings with your current pipeline

One Major problem with this pipeline is it's dependency on the color filter to sort the problens 
created by changing brightness and shadows in optional problem. In a real world situation I can 
easily see this failing. The lanes may not of these colors or under light they appear to be of a
completly diffrent color.

Second, while the approach for generating lines has worked for us here, it's a method that is still
very susiptible to noise and outliers.


### 3. Suggest possible improvements to your pipeline

Ist improvement would be to replace Color filter with a more roboust approach like histogram equlization
or adaptive thresholding. This would make the pipeline more robust to changes in light and brightness wihout 
expressly telling the lanes.

Second improvement would be to use a more robust way to generate a line, something like RANSAC will be more
robust against outliers and noise.
