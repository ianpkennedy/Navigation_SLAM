# Homework 4 - SLAM and Navigation - Ian Kennedy

To view demo videos from this assignment in browser, please use Ubuntu with Firefox.

This package uses the turtlebot to run SLAM, AMCL, and other mapping functionality in gazebo and in a real world scenario. Launch files in this exercise reference the custom turtlebot packages cloned from the instructions of the assignment. For the real world scenario, instruction for connecting to the turtlebot were followed and can be found at this URL:
https://nu-msr.github.io/me495_site/turtlebot3/turtlebot3.html

## Part 1.1

Entering`roslaunch hw4 start_slam.launch` is used to start the slam toolbox. It takes a `mode`  argument that determines whether to start the robot in gazebo, or start it in the real world. It is used to map an environment in gazebo when `mode` is `sim` , and mapped a portion of the NU robotics lab atrium when `mode` was `real`.

## Part 1.2

map_gazebo.yaml and map_gazebo.pgm were created using the `start_slam.launch` in the simulation mode, driving the turtlebot around with the teleop functionality. 
map_real.yaml and map_real.pgm were created with the same launch file using `mode` as `sim` when mapping the atrium.

## Part 1.3

In this part, entering in a terminal `roslaunch hw4 nav_stack.launch` was used to navigate to a goal set by a 2D Nav Point with the maps that were created in the previous step using the AMCL algorithm. For the gazebo run, `mode` was set to sim. For the real, `mode` was set to real. The result can be seen here below.

### Videos

Results:
Simulation: https://drive.google.com/file/d/1g5BZvHMnuymElRFyGapUSAPuXvw1y4cE/view?usp=sharing

Real: https://drive.google.com/file/d/1urOuR6geeY-Itanl7tOsTKWV-YjQS3ij/view?usp=sharing (RVIZ)
https://drive.google.com/file/d/1ZXKYW0PL2H5es6cp6yrlXBTyPfPYDVLc/view?usp=sharing (Real video)

## Part 2.1

In this part, the command `roslaunch hw4 slam_stack.launch` is used to navigate without preexisting map knowledge by setting a 2D Nav Point in Rviz using the slam_toolbox.  When `mode` is `sim` this is done in the house gazebo environment, when `mode` is `real` , this is done in the real world. Results can be found in the following videos:

### Videos

Results:
Simulation: https://drive.google.com/file/d/1-m79E1WmiWIipGCVSHYIwngtlsCo2SyB/view?usp=sharing

Real: https://drive.google.com/file/d/1uiVP0FNjU4mJHzQpoRA1lkKLdas_IOCD/view?usp=sharing (Real - I used my leg to block the turtlebot laser scanner from sensing the atrium column for the purposes of the task)

https://drive.google.com/file/d/1n02IEqK_Om48Xw8vnznP0R6p7vwcxAx-/view?usp=sharing (RVIZ)

## Part 2.2

In this part, SLAM was used to autonomously map an environment using random motion. 

Algorithm Explanation:
The algorithm used is a form of random motion. The explore node subscribes to the /odom topic in order to know the current position of the turtlebot. Then, the  node publishes a move to the /move_base_simple/goal for the async SLAM algorithm to use as a goal point to navigate to. The random point is in a +/- 1.0 meter range in the XY dimensions so as to be within range for the costmap. The theta orientation is randomized in the full -pi to +pi range. A timer is uses and is systematically reset in order to reset the goal to a new point. 

The resultant map is saved as expl.yaml and expl.pgm for the simulation run, and expl_real.yaml and expl.pgm for the exploration in the real world. 

To run this, run this command in a terminal : `roslaunch hw4 explore.launch` . set `mode` to real for a real turtlebot implementation, and sim for a gazebo run.


### Videos

Results:
Simultation: https://drive.google.com/file/d/1P_dztl_wqotQzEjrthXyyS6zd65DoEDS/view?usp=sharing 

Real: https://drive.google.com/file/d/1NnAmZZfnDMy0l2BsQP3srI0xzOFGCGuW/view?usp=sharing (Real)
https://drive.google.com/file/d/1rdfmnL2QKYL2eftitGWiRUwzxyPN8sj2/view?usp=sharing (RVIZ)

## Sources:

12/07:
For saving the maps throughout the assignment:
https://stackoverflow.com/questions/53545159/save-a-map-in-ros