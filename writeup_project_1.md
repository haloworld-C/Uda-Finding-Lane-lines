# **Finding Lane Lines on the Road** 

## Writeup of halo

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report



---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of TBD  main steps. 

First STEP, I detect the line both with white and yelow color using region mask and color mask

1. make a copy of the initial image
2. define the color mask(change the blue channel threshold to 50 to detect the yellow color)
3. define the region mask sa ladder-shaped(to avoid the detected line crossing)


Sencond Step: I detect the line with canny detection and hough-transform method.
1. tranfer the step 1 output image to grey scale with method **grayscale**
2. apply gaussian blur with method of **gaussian_blur**
3. apply edge detection with method of **canney**
4. detect lines in mask with method of **hough_lines**

Third Step: draw the detected lines in original image
1. revise the method of **draw_lines** to extent and average the detected lines with advised approach
2. limit the k scale to make sure the result is robust


At last, I used the two result image and draw the final line as below:

1. white line tested result:
<img src="output/white_successed.png" width="480" alt="white tested" />
2. yellow line tested result:
<img src="output/yellow_successed.png" width="480" alt="yellow tested" />

Ater I tested all test images provided by tuning parameters, I tested the vedios, it seems that the vedio is much difficult. I have to re-tuning the parameter and revise the defined region mask. 

Finaly I was satisfied with the vedio results.


My feedback:

*issue 1: debugging error*

    1. there is a directory name error
    2. encountered a error of lacking of ffmped.linux64 software. In order to solve this problem I dived in the docker kit of "carnd-term1-starter-kit". It stucked me two days, but when I fixed this, I found the docker mechanism is quite a amazing technology!
    3. I also encontered some error with python function and fix them.
*issue 2: tuning the patameter in program when tested vedios*

    1. encoutered the line shape as below. I fixed this by limiting the k scale(< 0.1)
   
<img src="./output/yellow_issue.png" width="480" alt="yellow issue" />
    2. When tested the challenge video, I found the distraction of moving cars is a big issue. I improve the performance with narrowing the region mask. 




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is moving car in beside lane, the line detected is not stable. 

Another shortcoming could be when the light is not good(in challenge there are tree shadow) , the current pipeline can not detect lines.

Last but not least, the current pipeline is really relying on the color mask, this will lose some robust performence.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to :
As we know, the line on road is continuous, when we have a high confidence level of detected line, then we can make a further limit of "k" of line.

Another potential improvement could be :
the distance between the lane line bottom and center point of image bottom line can be also a limit when deal with draw_lines.
