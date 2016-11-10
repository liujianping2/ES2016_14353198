# lab5����װROS
#### SLAM(simultaneous localization and mapping ͬʱ��λ�뽨ͼ)������˵������·
#### ROS �������SLAM�㷨����Ӧ�����ݼ���
#### �����������ʵ��������ڰ�ͼ������ROS��
Robot operation system��ROS����һ�׿�ܣ��ײ��ṩӲ���������������֧��ͨ�õ��ļ���ʽ��
����ROS��ǰ������Ubuntu�����û������Ҫ����Ubuntu���ҵ�ʵ��������Ubuntu��ǰ���µġ�
����UbuntuҪ���������restricted , universe �� multiverse �����Դ��
#### ROS��װ��

Ubuntu 14.04 �� 15.04 ��ο���  
<http://wiki.ros.org/jade/Installation/Ubuntu>  
Ubuntu 15.10 , 16.04 ��ο���   
< http://wiki.ros.org/kinetic/Installation/Ubuntu>

#### �ҵ�����Ubuntu 14.04.4�����õģ�
##### 1��������Դ��sources.list , �������Դ�Ĵ������£�  
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' `  
һ���������ȷ�����Դ������ϵͳ��֪��ȥ�������س��򣬲����������Զ���װ�����


##### 2������������Կ  
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`  

##### 3����װ  
����ȷ�����Debian����������������µġ�Debian�ƻ���һ�������ڴ���һ�����ɲ���ϵͳ�ĺ�����֯���������������������ϵͳ��Ϊ Debian��DebianϵͳĿǰ����Linux�ں˻���FreeBSD�ںˡ�  
`sudo apt-get update`  
Desktop-Full Install:  
��ROS������಻ͬ�ĺ�����͹��ߣ���������ȫ��װ��Ҳ���Ը����Լ���Ҫ��ֱ�װ����ȫ��װʱ�Ĺ��߰���ROS��rqt�����ӻ�����rviz��ͨ�û����˿�robot-generic libraries��2D����stage����3D����Gazebo�����滷��2D/3D simulators���������ܰ���navigation and 2D/3D���ƶ�����λ����ͼ���ơ���е�ۿ��ƣ�����֪��perception�����Ӿ��������״RGB-D����ͷ�ȣ���  
`sudo apt-get install ros-jade-desktop-full`   

##### 4����ʼ��rosdep  
rosdep�����ܹ�ʹ�������İ�װһЩϵͳ���������������ROS��һЩ��Ҫ����������Ҳ��Ҫrosdep��  
`sudo rosdep init`  
`rosdep update`  

##### 5�����û���  
���ROS�Ļ�����������������������µ�shellʱ�����bash�Ự�л��Զ���ӻ���������  
`echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc`  
`source ~/.bashrc`  
���ֻ����ĵ�ǰshell�Ļ��������Լ��룺  
`source /opt/ros/jade/setup.bash`  

##### 6����ȡrosinstall  
rosinstall��ROS�о���ʹ�õ������й��ߣ����ǵ����ַ��ġ���ʹ���ܹ�ʹ��һ��������������ROS����������Դ��������  
`sudo apt-get install python-rosinstall`  

##### 7����ȡ�Ѱ�װ�������Դ����  
�����֪��ÿ�����Ĳֿ��λ�ã���֪������Ի�����еĴ��롣���Ǽ�ʹ�����о���Ŀ�����Ա��˵��ͨ�����ѴﵽĳЩ������ȷά���Ŀ⡣���⣬��ĳЩ����£���ֻ���ȡ�Ѱ�װ�汾�����������Դ�����������ķ������ʺ���Щ�����

?�����ڵ�ROS���ݳ��ǵ����磩��������ͨ�����������ᵽ�ķ�ʽ��á�


?����ֻ��apt-getԴ��sudo����Ҫ�����¡�����������Ҫ��ȷָ��deb-src��Ŀ�ȡ���ӷ����������˷�����������е������ļ���Ҳ����û�а�װ�ڰ�װ�����еĶ���������CMakeLists.txt������  
`apt-get source ros-jade-laser-pipeline`  


#### ���ˣ��������ROS �������ˡ�

### ʵ����� �����ʵ��ȽϹ̶��������ǰ�����ҳ���Ĳ���һ��һ��ʵ�֣�û��ʲô����