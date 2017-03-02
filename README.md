# phantomx_arm
Phantomx pincher arm package

To add the phantomx arm to a turtlebot you need to edit a number of files.

First make sure you have downloaded the turtlebot packages, you can do this through deb, but you will have to go through and edit the files in your opt/ros/indigo/ setup. It is much easier to do so by downloading the correct packages (indigo) into your catkin_ws/src.


Open the phantomx_arm.urdf.xacro file and remove or edit out the link 'base_link'. This is because we are going to tell the arm to become attached to the turtlebot top plate link.

```
<!-- As we don't have here a turtlebot base, add a base_link link as its location reference -->
    <!--
    <link name="base_link"/>
     -->
<!-- Turtlebot arm macro -->
```

Next open up the 'kobuki_hexagons_kinect.urdf.xacro' file and add:
```
<xacro:include filename="$(find phantomx_arm_description)/urdf/phantomx_arm.xacro"/>
```
This will run the xacro which will then add the arm. To be hoenst I'm not sure whether you just can't set it up using the previous file, but oh well.

This is for a turtlebot setup that has:

- Base      : kobuki
- Stacks    : hexagons
- 3d Sensor : kinect

Check your turtlebot environmental params using:
```
env | grep TURTLEBOT
```
This should allow you to check what base, sensors etc are being loaded when building the robot model. If you need to change this then you will have to edit your bash.src using:
```
echo "export TURTLEBOT_3D_SENSOR=kinect" >> .bashrc
```
Also if you actually have a real arm physically attached then you can add:
```
<include file="$(find phantomx_arm_bringup)/launch/arm.launch"/>
```
to your robot.launch file
