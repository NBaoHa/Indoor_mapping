## Prepping Raspberry Pi
After setting remote development using VNC and/or SSH via VScode, some packages needs to be installed to act as a framwork for any software developments


#### ROS Installation (Robotic Operating System)
open terminal then:
```
sudo apt update
sudo apt install ros-noetic-desktop 
sudo apt-get install build-essential
```

```
echo "source/opt/ros/noetic/setup.bash">> ~/.bashrc
source ~/.bashrc
```

 #### Connect Lidar and verify port
 
connect lidar to raspberry pi through the adapter (Micro USB to USB 2.0) 

verify port by and change permission by:
```
ls -l /dev| grep ttyUSB
sudo chmod 666 /dev/ttyUSB0
```

#### RPlidar ros package
if you have catkin_ws already then skip the code block below, else:
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
```
After navigating to the catkin workspace (catkin_ws)
```
catkin_init_workspace
echo "source $HOME/catkin_ws/devel/setup.bash">>~/.bashrc
cd src
sudo git clode https://github.com/slamtec/rplidar_ros.git
```
After instllation of the package (or any package),
```
cd ~/catkin_ws/
catkin_make
```
there might be a CMakeLists in catkin_ws which can prevent the catkin_make to not work, unlink can be used to delete that cmakelist file 
then run catkin_make again
``` 
unlink /home/ubuntu/catkin_ws/CMakeLists.txt
```

#### Test Run Lidar
have to run this everytime after opening a new terminal and before running any ROS commands
```
source devel/setup.bash
```
View Lidar with through ROS
```
roslaunch rplidar_ros view_rplidar.launch
```
Ctrl-C or Cmd-C to quit

#### Install Hector Slam 
```
cd ~/catkin_ws/src
sudo git clone https://github.com/tu-darmstadt-ros-pkg/hector_slam.git
cd ~/catkin_ws/
catkin_make
```

### Run Slam
Because we don't have an Inertia Measurement Unit, we have to modify the launch files 
to enable movement tracking (localization) when we are actively measuring. To modify, we need to go to ____ launch file in  ____ directory.
```

```
then go to _____launch file in ____ directory

terminal 1:
  ```
  roscore
  ```
terminal 2: 
  ```
  cd ~/catkin_ws/
  source devel/setup.bash
  roslaunch rplidar_ros rplidar.launch
  ```
terminal 3:
 ```
 cd ~/catkin_ws/
 source devel/setup.bash
 roslaunch hector_slam_launch tutorial.launch 
 ```
 tutorial.launch can be changed to the modified launch file name
 
 
 
There you have it, 
 
with the RPlidar and Raspberry pi working, you can walk around holding the lidar to map out the indoor space.
But to make things more interesting, why not sit at a chair and use an RC car instead to do the moving around....
we will move a step further in utilizing a freenove 4WD car

