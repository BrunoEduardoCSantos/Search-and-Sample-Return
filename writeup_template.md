## Project: Search and Sample Return
---

### Notebook Analysis
#### 1. Detection of obstacles and rock samples using image processing 

For achieving the obstacles detection (color_theresh_obstacles function) it was applied the complementary condition for obtaining navigable terrain, i.e, threshold of RGB > 160 does to identify ground pixels. 

Here is an example how does look the constrast between navigable terrain and obstacles

![Obstacle](https://github.com/BrunoEduardoCSantos/Search-and-Sample-Return/blob/master/misc/obst.jpeg)

In order to detect rock samples, it was applied a RGB thereshold with the following ranges, respectively: lower = [90, 90, 0]  ;upper = [160, 160, 80] .

The following picture shows clearly the rock detected in a binary format.

![Rock_samples](https://github.com/BrunoEduardoCSantos/Search-and-Sample-Return/blob/master/misc/rock.jpeg)

#### 2. Image processing steps to create a map of pixels identifying navigable terrain, obstacles and rock samples into a worldmap
The process to create a map combining navigable terrain , obstacles and rock samples into a worldmap is composed by following steps:

* Define the source and target points to apply transformation from rover perspective to top-side one 
* Use that warped image and feed to theresholds obtained in previous section in order to get the map of navigable terrain, obstacles and rock samples
* Calculate pixel values in rover-centric coords 
* Calculate pixel values in world coords 
* Overlay worldmap with ground truth map

To visualize in further detail the first 3 steps are depicted in the following images:
![Transf](https://github.com/BrunoEduardoCSantos/Search-and-Sample-Return/blob/master/misc/Plot.jpeg)

Finally, it was created a sample ![video](https://github.com/BrunoEduardoCSantos/Search-and-Sample-Return/blob/master/output/test_mapping.mp4) of combined map of rover navigating.

### Autonomous Navigation and Mapping

#### 1. Decision and Perception steps 

In order to achieve **perception process** the following set of functions were used (functions compiled in **perception.py**):
* **color_thresh** : find the terrain pixels using rover camera images
* **color_theresh_rock** : find the rock samples using rover camera images
* **rover_coords** : convert from image coords to rover coords
* **to_polar_coords** : convert to radial coords in rover space
* **rotate_pix** : map rover space pixels to world space
* **translate_pix** : scale from ground truth scale to rover camera images
* **pix_to_world** : apply rotation and translation (and clipping)
* **perspect_transform** : perform a perspective transform

In order to achieve **decision step** the following modifications were applied (inside  **decision.py**):
* 


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  



![alt text][image3]


