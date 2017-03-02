# ND_SDC_LaneFollow
self driving cars project1 lane follow
Project writeup for Project 1, Finding lane Lines
Greg Luker
February  2016


 In this project we will write a program to detect lane lines on .jpg and .mpeg files.
Reflection
A significant amount of time was spent getting the programming environment installed then debugged. Several modules were not installed that had to be tracked down. One module had to be downloaded special then copied and installed manually.

1. Pipeline Description
First I made a copy of the image that was used at the end for drawing the lines.
Then there were five function calls to functions that were provided.

The first function converted the  image to Grayscale  cv2.cvtColor(image, cv2.COLOR_RGB2GRAY) 
Then the function     image = gaussian_blur was called to

Next canny(image, 110, 150)  function was called to to perform the canny function.

 gaussian_blur(i

 region_of_interest is used to restrict the lines we will look at that are lower on the horizon where the lane lines are.
    line_image = np.copy(image)*0 # creating a blank to draw lines on

   hough_lines(image, rho, theta, threshold, min_line_len, max_line_gap)
hough function will acall draw_lines which will do most of my processing of the lines to detect the lane lines.

The inputs to the THIRD FUNCTION TOOK THE LONGEST TO TWEAK FOR FINDING LANE LINES
region_of_interest(image, vertices)

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...
In order to get rid of the horizontal and verticl lines I throw away all lines that have a slope too steep or too flat. Only store lines with slope >= minSlope and slope < maxSlope:
Next I keep a running average of the left lane slope and right line slope.
The Averae slope is used to extend the lines up to preset line and down to the bottom of the screen.



I was able to get rid of most of the horizontal lines introduced by the more complex video in the challenge video.


2. Identify potential shortcomings
CURRENTLY MY PROGRAM WORKS FINE WITH THE the solidWhitRight and SolidYellowLeft Mpeg video files. The Challenge.mpg is curently not working very well.
 
 If there is too much noise the averaging function can get into trouble and can take a while to reset.
 
 
One potential shortcoming would be what would happen when ...

Another shortcoming could be working with different colors of asphault, wet roads and low light condtions

3. Suggest possible improvements to your pipeline
On the challenge video there are several things that challenge the lane finding. The curve, missing lane marking and heavy shadows and vegitation.
To make the software much more robust it would really help to have a sophisticated lane average in place. In an acutual car it would be nice to have multiple lane finding routines running at the same time. When one falls short the other could be used while needed.

 

Another potential improvement could be to ...
