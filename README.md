# ND_SDC_LaneFollow
self driving cars project1 lane follow
Project writeup for Project 1, Finding lane Lines
Greg Luker
Most work was done in Feb and early March.
Submitted April 21 2017.


 In this project I  wrote a program to detect lane lines on .jpg and .mpeg files.
 
Reflection
A significant amount of time was spent getting the programming environment installed then debugged. Several modules were not installed that had to be tracked down. One module had to be downloaded special then copied and installed manually.

This was my first real project using  Python so it was quite educational.

1. Pipeline Description
First I made a copy of the image that was used at the end for drawing the lines.
Then there were five function calls to functions that were provided.

The first function converted the  image to Grayscale  cv2.cvtColor(image, cv2.COLOR_RGB2GRAY).
Converting to greyscale makes it easier to find edges and speeds up the processing.

Next canny(image, 110, 150)  function was called to to perform the canny function.

From https://en.wikipedia.org/wiki/Canny_edge_detector
Canny edge detection is a technique to extract useful structural information from different vision objects and dramatically reduce the amount of data to be processed. It has been widely applied in various computer vision systems. Canny has found that the requirements for the application of edge detection on diverse vision systems are relatively similar. Thus, an edge detection solution to address these requirements can be implemented in a wide range of situations.
Among the edge detection methods developed so far, Canny edge detection algorithm is one of the most strictly defined methods that provides good and reliable detection.

Then the function gaussian_blur was called to reduse the noise. This will help prevent detecting too many false lines.

The inputs to the fourth function took the longest to tweek for finding the lane lines.
 region_of_interest is used to restrict the lines we will look at that are lower on the horizon where the lane lines are.
    line_image = np.copy(image)*0 . We can also try to reduce the reflections from the hood.

Next the super critical hough_lines() function is called.

The purpose of the Hough transform is to find imperfect instances of objects within a certain class of shapes by a voting procedure. This voting procedure is carried out in a parameter space, from which object candidates are obtained as local maxima in a so-called accumulator space that is explicitly constructed by the algorithm for computing the Hough transform.
   hough_lines(image, rho, theta, threshold, min_line_len, max_line_gap)

In order to draw a single line on the left and right lanes, I modified the draw_lines() function.
In order to get rid of the horizontal and vertical lines, I throw away all lines that have a slope too steep or too flat. I Only store lines with slope >= minSlope and slope < maxSlope:
Next I keep a running average of the left lane slope and right lane slope.
The Average slope is used to extend the lines up to a preset line and down to the bottom of the screen.


I was able to get rid of most of the horizontal lines introduced by the more complex video in the challenge video.


2. Identify potential shortcomings

Befor I started keeping a running average for the slope lines The Challenge.mpg was  not working very well. Now that I am keeping a running avarage of the slopes of the lane lines it is working much better.
 
If there is too much noise the averaging function can get into trouble and can take a while to reset.
 
One potential shortcoming is that it takes a while for my program to get the averaging up and running.

Another shortcoming could be working with different colors of asphault, wet roads and low light condtions

3. Suggest possible improvements to your pipeline
On the challenge video there are several things that challenge the lane finding. The curve, missing lane marking and heavy shadows and vegitation.
To make the software much more robust it would really help to have a sophisticated lane average in place. In an acutual car it would be nice to have multiple lane finding routines running at the same time. When one falls short the other could be used while needed.

4. Use of Spyder instead of Jupyter notebook
 I was having a hard time getting Jupyter notebook to run so I used Spyder for all my developement.
 
 As you can see by the dates I had the majority of this project completed over a month ago. I was in the process of learning Git to clean up the files, but it took far too long so I am submitting in its current state.
 
 Conclusion
 
 This project took far longer than anticipated due the learning curve with python and Git and the trouble with getting all the tools installed and working. I beleive I learned quite a bit on this project and there is far more that could be done, but I need to get on to the other projects.
 The final code works far better than the early code without the running average for the slope.
 
 
