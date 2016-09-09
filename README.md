# turtlebot_getting_started
*PC refers to your Linux machine, turtlebot is the Odroid on-board computer*
Switch on the turtlebot : allow the onboard Odroid Xu4 to boot
The netword SSID should appear on the list of networks as turtlebotJ, connect to this.
`password is turtlebotJ`
 To find your ip address, type 'ifconfig'. The wireless configuration should tell you it is in the form of `192.168.100.10x`


##Creating your PC as as ROS node
Change the last lines of the .bashrc file on the PC to:
'''
export ROS_MASTER_URI=http://192.168.100.100:11311
export ROS_HOSTNAME=192.168.100.102
export ROS_IP=192.168.100.102
'''
(assuming your PC is 192.168.100.102 otherwise change it to the results of your ifconfig)
Now, .bashrc is run every time you open Terminal. So you can closes the terminal, or type `source .bashrc`

Now 'ssh' into the turtlebot.
`ssh 192.168.100.100`
`password:ros`

On the turtlebot, launch the following:
  `roslaunch turtlebot_bringup minimal.launch`
You should hear a rising tone and some positive messages on terminal (ignore the battery warning)
In another terminal on the turtlebot (ssh in again):
`	roslaunch turtlebot_navigation gmapping_demo.launch`
and another terminal on turtlebot, to allow the robot to operate from the keyboard
`roslaunch turtlebot_teleop keyboard_teleop.launch`

On the PC:
`rviz rviz`
Select (or add) laser scan, robot model, marker array, and map.
_A more in depth tutorial is at [learn.turtlebot.com](http://learn.turtlebot.com)
Drive the robot using the keys (ensure the _keyboard_teleop.launch_ window is active).
Save the map using:
`rosrun map_server map_saver -f /tmp/my_office`
###Autonomous driving
Stop the `roslaunch turtlebot_navigation gmapping_demo.launch`
and run:
`roslaunch turtlebot_navigation amcl_demo.launch map_file:=/tmp/my_office.yaml`


