# lab5：安装ROS
#### SLAM(simultaneous localization and mapping 同时定位与建图)，简单来说就是认路
#### ROS 上有许多SLAM算法及对应的数据集。
#### 我们这次做的实验就是在乌班图下配置ROS。
Robot operation system（ROS）是一套框架，底层提供硬件驱动，软件层面支持通用的文件格式。
配置ROS的前提是有Ubuntu，如果没有首先要按照Ubuntu。我的实验是在有Ubuntu的前提下的。
配置Ubuntu要求允许接受restricted , universe 和 multiverse 的软件源。
#### ROS安装：

Ubuntu 14.04 ， 15.04 请参考：  
<http://wiki.ros.org/jade/Installation/Ubuntu>  
Ubuntu 15.10 , 16.04 请参考：   
< http://wiki.ros.org/kinetic/Installation/Ubuntu>

#### 我的是在Ubuntu 14.04.4下配置的：
##### 1、添加软件源到sources.list , 设置软件源的代码如下：  
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' `  
一旦添加了正确的软件源，操作系统就知道去哪里下载程序，并根据命令自动安装软件。


##### 2、设置您的密钥  
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`  

##### 3、安装  
首先确认你的Debian的软件包索引是最新的。Debian计划是一个致力于创建一个自由操作系统的合作组织。我们所创建的这个操作系统名为 Debian。Debian系统目前采用Linux内核或者FreeBSD内核。  
`sudo apt-get update`  
Desktop-Full Install:  
在ROS中有许多不同的函数库和工具，建议是完全安装，也可以根据自己的要求分别安装。完全安装时的工具包括ROS、rqt、可视化环境rviz、通用机器人库robot-generic libraries、2D（如stage）和3D（如Gazebo）仿真环境2D/3D simulators、导航功能包集navigation and 2D/3D（移动、定位、地图绘制、机械臂控制）、感知库perception（如视觉、激光雷达、RGB-D摄像头等）。  
`sudo apt-get install ros-jade-desktop-full`   

##### 4、初始化rosdep  
rosdep不仅能够使你更方便的安装一些系统依赖程序包，而且ROS的一些主要部件的运行也需要rosdep。  
`sudo rosdep init`  
`rosdep update`  

##### 5、设置环境  
添加ROS的环境变量，这样，当你打开你新的shell时，你的bash会话中会自动添加环境变量。  
`echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc`  
`source ~/.bashrc`  
如果只想更改当前shell的环境，可以键入：  
`source /opt/ros/jade/setup.bash`  

##### 6、获取rosinstall  
rosinstall是ROS中经常使用的命令行工具，它是单独分发的。它使您能够使用一个命令轻松下载ROS软件包的许多源代码树。  
`sudo apt-get install python-rosinstall`  

##### 7、获取已安装软件包的源代码  
如果你知道每个包的仓库的位置，你知道你可以获得所有的代码。但是即使对于有经验的开发人员来说，通常很难达到某些包的正确维护的库。此外，在某些情况下，您只想获取已安装版本的软件包的来源。这里描述的方法最适合这些情况。

?在早期的ROS（据称是电或更早），您可以通过本问题中提到的方式获得。


?现在只是apt-get源（sudo不需要）如下。你甚至不需要明确指定deb-src条目等。这从服务器下载了发布的软件包中的所有文件（也包括没有安装在安装规则中的东西（例如CMakeLists.txt））。  
`apt-get source ros-jade-laser-pipeline`  


#### 到此，就完成了ROS 的配置了。

### 实验感想 ：这次实验比较固定化，就是按照网页给的步骤一步一步实现，没有什么错误。