[//]: # (Image References)

[image1]: ./examples/YW.gif "White Yellow Mask"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:
First, I apply a HSV color filter, which enhances the colors yellow and white.  
![alt text][image1]
The advantage of using a HSV color filter over one in RGB is that it's easier to describe a
color range in HSV.

Second, I grayscale this image we acquire from the color filter:
![Alt text][/examples/GR.gif?raw=true]

If you'd like to include images to show how the pipeline works, here is how to include an image: 




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
