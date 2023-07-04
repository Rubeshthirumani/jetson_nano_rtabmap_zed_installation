# Installing RTabMap and ZED Wrapper in Jetson Nano 4GB L4T

[![robotoai](https://robotoai.com/wp-content/uploads/2020/11/cropped-logo-5.png)]()


`Steps to install RTabMap and ZED Wrapper in jetson nano`

- Flash a new SD Card with Jetson image
- Follow this [GETTING STARTED WITH NEW JETSION NANO AND HOHW TO WRITE A SD CARD IMAGE FILE](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit) 
- Follow this [INSTALL ROS IN JETSON NANO](https://www.stereolabs.com/blog/ros-and-nvidia-jetson-nano/)


## ROS distribution

```sh
sudo apt install ros-$ROS_DISTRO-rtabmap-ros
```

```sh
sudo apt install ros-$ROS_DISTRO-rtabmap ros-$ROS_DISTRO-rtabmap-ros
```

# Install RTAB-Map standalone libraries. Do not clone in your Catkin workspace.
```sh
cd ~
git clone https://github.com/introlab/rtabmap.git rtabmap
cd rtabmap/build
cmake ..  [<---double dots included]
make -j1 
sudo make install
```
# Install RTAB-Map ros-pkg in your src folder of your Catkin workspace.
```sh
cd ~/catkin_ws
git clone https://github.com/introlab/rtabmap_ros.git src/rtabmap_ros
catkin_make -j1
```

# Clone ZED ROS Wrapper and ZED ROS Interfaces into your catkin workspace
```sh
 cd ~/catkin_ws/src
git clone --recursive https://github.com/stereolabs/zed-ros-wrapper.git
cd ../
rosdep install --from-paths src --ignore-src -r -y
catkin_make -DCMAKE_BUILD_TYPE=Release
```

`Note: If your receive any cmake error related to CV Bridge, refer this` [REFER OPENCV CV BRIDGE ERROR ](https://answers.ros.org/question/199279/installation-from-source-fails-because-of-cv_bridge-include-dir/) 
## This solved for me
```sh
sudo ln -s /usr/include/opencv4/opencv2/ /usr/include/opencv
```
This both (up and down syntaxes) will solve this issue permanently. Kindly utilize this according to the error arised.
```sh
sudo apt remove ros-melodic-cv-bridge
```
[DOWNLOAD THE VISION OPENCV - MELODIC BRANCH AS ZIP FILE](https://github.com/BrutusTT/vision_opencv.git ) 
[DOWNLOAD THE image_transport_plugins - MELODIC BRANCH AS ZIP FILE](https://github.com/ros-perception/image_transport_plugins) 

#### Unzip both above mentioned packaes and keep it inside src folder of your catkin_ws
```sh
cd catkin_ws/src
catkin_make
```
# Clone ZED ROS Exmples into your catkin workspace
```sh
cd ~/catkin_ws/src
git clone https://github.com/stereolabs/zed-ros-examples.git
cd ../
rosdep install --from-paths src --ignore-src -r -y
catkin_make -DCMAKE_BUILD_TYPE=Release
```
`Now, we shall ready to start rtabmapping`
