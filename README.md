# Project3-WhereAmI
This project is about implementing the most powerful localization algorithm for a mobile robot in arbitrary space using Adaptive Monte Carlo localization (AMCL) with pre-designed map.


## Overview  
This Projects mainly focus on implemention of the most advanced localization algorithm(Adaptive Monte Carlo Localization) to localize a mobile Robot's pose in arbitrary location as it travels through predefined set of waypoints. This entire project is developed within ROS and the robots pose is finally obtained after fine tuning the tuning parameters in AMCL. The main steps involved in compiling AMCL in ROS is described below:
* Design a mobile Robot and building in a custom Gazebo world by launching them using respective ROS packages.
* Use pgm_map_creator package to create maps for kinetic (use gmapping for noetic or other higher versions) and this results in a picture that can be viewed in image viewer and it is sent as an input to the AMCL package. This map mainly contains dark pixels that means there are obstacles and white pixels means the free space. 
* Create a ROS AMCL package and it mainly contails3 nodes. They are 1. Map Server node(to take the map file as input to robot), 2. AMCL node(to read the map file and localize the robot by fine tuning the various parameters), and 3. Move base node(robot will navigate to that goal position when we try to control the robot).
* To further control the robot we can use Tele-Operation / Navigation Stack using keyboard and also using ROS Rviz settings.
* Launch all the respective nodes and move the robot (either using keyboard or 2D Nav Goal) and explore the tuning parameters and adjust them to localize the robot accordingly. 

## Prerequisites/Dependencies  
* Gazebo >= 7.0  
* ROS Kinetic  
* ROS navigation package  
```
sudo apt-get install ros-kinetic-navigation
```
* ROS map_server package  
```
sudo apt-get install ros-kinetic-map-server
```
* ROS move_base package  
```
sudo apt-get install ros-kinetic-move-base
```
* ROS amcl package  
```
sudo apt-get install ros-kinetic-amcl
```
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
  
## Setup Instructions (abbreviated)  
1. Meet the `Prerequisites/Dependencies`  
2. Open Ubuntu Bash and clone the project repository  
3. On the command line execute  
```bash
sudo apt-get update && sudo apt-get upgrade -y
```
4. Build and run your code.  

## Project Description  
Directory Structure  
```
.Where-Am-I                                    # Where Am I Project
├── catkin_ws                                  # Catkin workspace
│   ├── src
│   │   ├── ball_chaser                        # ball_chaser package        
│   │   │   ├── launch                         # launch folder for launch files
│   │   │   │   ├── ball_chaser.launch
│   │   │   ├── src                            # source folder for C++ scripts
│   │   │   │   ├── drive_bot.cpp
│   │   │   │   ├── process_images.cpp
│   │   │   ├── srv                            # service folder for ROS services
│   │   │   │   ├── DriveToTarget.srv
│   │   │   ├── CMakeLists.txt                 # compiler instructions
│   │   │   ├── package.xml                    # package info
│   │   ├── my_robot                           # my_robot package        
│   │   │   ├── config                         # config folder for configuration files   
│   │   │   │   ├── base_local_planner_params.yaml
│   │   │   │   ├── costmap_common_params.yaml
│   │   │   │   ├── global_costmap_params.yaml
│   │   │   │   ├── local_costmap_params.yaml
│   │   │   ├── launch                         # launch folder for launch files   
│   │   │   │   ├── amcl.launch
│   │   │   │   ├── robot_description.launch
│   │   │   │   ├── world.launch
│   │   │   ├── maps                           # maps folder for maps
│   │   │   │   ├── map.pgm
│   │   │   │   ├── map.yaml
│   │   │   ├── meshes                         # meshes folder for sensors
│   │   │   │   ├── hokuyo.dae
│   │   │   ├── rviz                           # rviz folder for rviz configuration files
│   │   │   │   ├── default.rviz
│   │   │   ├── urdf                           # urdf folder for xarco files
│   │   │   │   ├── my_robot.gazebo
│   │   │   │   ├── my_robot.xacro
│   │   │   ├── worlds                         # world folder for world files
│   │   │   │   ├── empty.world
│   │   │   │   ├── myworld.world
│   │   │   ├── CMakeLists.txt                 # compiler instructions
│   │   │   ├── package.xml                    # package info
│   │   ├── pgm_map_creator                    # Create pgm map from Gazebo world file for ROS localization
│   │   │   ├── maps
│   │   │   │   ├── map.pgm                    # map files of office.world, generated by pgm_map_creator
├── my_ball                                    # Model files 
│   ├── model.config
│   ├── model.sdf
├── localization_screenshots                                  
```   

## Following the instructions below to run the ROS AMCL Project:
* Clone this repository
```
git clone https://github.com/daddalasaipraveen/Project3-WhereAmI.git
```
* Open the repository and make  
```
cd /home/workspace/P3-Where-Am-I/catkin_ws/
catkin_make
```
* Launch my_robot in Gazebo to load both the world and plugins  
```
roslaunch my_robot world.launch
```  
* Launch amcl node  
```
roslaunch my_robot amcl.launch
```  
## Testing  
The mobile robot can be navigated using two features and hence we have two options to control your robot while it localize itself here: 
  * Send navigation goal via RViz  
  * Send move command via teleop package.  
Navigate your robot, observe its performance and tune your parameters for AMCL. 

## Here are some final pictures of the Project:
The following figues indicate shows how the Robot is localized using Adaptive Monte Carlo Localization algorithm inside the Gazebo simulation within ROS.
![Screenshot from 2023-01-20 23-05-18](https://user-images.githubusercontent.com/89826843/213850199-71f10b28-af6c-4fcf-a35e-b1d82d0c3cb4.png)
![Screenshot from 2023-01-20 23-05-39](https://user-images.githubusercontent.com/89826843/213850261-48bd073e-4d26-4d7b-aba2-07217b00767b.png)
![Screenshot from 2023-01-20 23-05-56](https://user-images.githubusercontent.com/89826843/213850293-1aa3b88e-3119-4a71-9e72-1996fbce0972.png)
![Screenshot from 2023-01-20 23-07-50](https://user-images.githubusercontent.com/89826843/213850323-825c379c-958a-4937-9443-ef1875e29477.png)
![Screenshot from 2023-01-20 23-08-06](https://user-images.githubusercontent.com/89826843/213850355-24087561-925b-48ff-aec1-e365fc774cf9.png)
![Screenshot from 2023-01-20 23-11-25](https://user-images.githubusercontent.com/89826843/213850360-42def10e-cd05-48fe-9038-6bb120233cef.png)

Thank you for looking into my github repo and I will be happy to take any comments.
