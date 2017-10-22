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

* **Define source and destination points for perspective transform**
* **Apply perspective transform** : apply coordinates transformation for a top-side view ny defining source points and prefered final destination points in order to have an alignement with world map
* **Find the navigable terrain , rock samples and obstacles pixels**: apply a thereshold on RGB components as mention in previous section
* **Calculate pixel values in rover-centric coords**: calculate navigable terrain and obstacle coordinates in rover centric coordinates so that rover can make decision where to navigate
* **Calculate pixel values in world coords**: calculate navigable pixels in world map perspective resulting aligning map from perspective transform with ground truth map by rotating an angle equal to yaw angle and scale to ground truth map scale  
* Use channels red, blue and green to overlay worldmap with world map points which rover has crossed it, where red is for obstacles, to rock samples and blue to navigable terrain


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

In order to achieve **decision step** the following modification was applied (changed parameters **driver_rover.py**):
* modify start and stop number of navigable pixels to 500 and 600 , respectively.

#### 2. Settings of simulator and approach taken to launch autonomous rover 

The simulator settings used during autonomous mode were following (resolution and graphics quality set on launch):
* **Screen Resolution** : 800 X 600
* **Graphic Quality** :  Good

The approach taken in this project was using the two following references frames: 
* Rover centric coordinates
* General coordinates from top side view

In order to obtain rover centric coordinates, it was applied a perspective transformation to rover camera images in order to get top-side view of rover. Afterwards, a gride of terrain was obtained to map the terrain using rover camera images. From this map, it was computed the coordinates of image using rover coordinates , where the rover was considered to be centered in the middle left of image. In this case, it could be used a rover image center coordinates. Also, it is important to mention is transformation was done considering pitch and roll equal to zero, which influence the map fidelity. Finally, to obtain an aligned reference frame with the world frame it was applied a rotation angle (yaw angle) around z-axis.
The importance of having both reference frames is to allow the rover not be trapped in a loop or to avoid repeat search space. In further detail, one improvement could be made would be not repeat search space in order to navigate faster through environment.
Finally, so achieve which direction rover should take, it was computed the polar angle using rover centric image coordinates and use the mean of those angles to get the direction where rover should navigate. In this step, maybe it could be used an angle gaussian distribution of most probable direction to take.


