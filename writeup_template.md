## Project: Search and Sample Return
---

### Notebook Analysis
#### 1. Detection of obstacles and rock samples using image processing 

For achieving the obstacles detection (color_theresh_obstacles function) it was applied the complementary condition for obtaining navigable terrain, i.e, threshold of RGB > 160 does to identify ground pixels. 

Here is an example how does look the constrast between navigable terrain and obstacles

![alt text][https://github.com/BrunoEduardoCSantos/Search-and-Sample-Return/blob/master/misc/obst.jpeg]

In order to detect rock samples, it was applied a RGB thereshold with the following ranges, respectively: lower = [90, 90, 0]  ;upper = [160, 160, 80] .

The following picture shows clearly the rock detected in a binary format.

![alt text][https://github.com/BrunoEduardoCSantos/Search-and-Sample-Return/blob/master/misc/rock.jpeg]

#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 
And another! 

![alt text][image2]
### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  



![alt text][image3]


