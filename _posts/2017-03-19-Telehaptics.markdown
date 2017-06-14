---
title: Geomagic Touch Driven Control of a Robotic Arm
subtitle: Human-Machine Interaction
layout: default
modal-id: 5
date: 2017-03-19
thumbnail: telehapticstemp.png
alt: image-alt
project-date: January 2017 - May 2017
client: Northwestern MSR
category: Human-Machine Interaction
description: An Intuitive Interface which Allows Human Users to Feel What Robots Feel
---
<center><h3>Overview</h3></center>
Haptic perception is an intrinsic facet of the somatosensory system which grants humans the ability to discern valuable information about the shape, orientation, and texture of objects in the world. Without it, even simple motor tasks can become frustratingly difficult to perform. The lack of tactile feedback in commercially-available prosthetics and teleoperated devices is a debilitating obstacle which prevents amputees, technicians and surgeons from moving naturally and dexterously with artificial limbs.

Telehaptics is a ROS Python package which brings to life a basic haptic interface using a Baxter research robot and the Geomagic Touch. When the stylus of a Touch is moved, Baxter's right arm will trace the same motions performed. If an external force is applied to the arm, the Touch will remotely apply the same forces to the user's hand. Together, these components form a closed-loop biofeedback system which enables users to experience something akin to telekinesis.

Note, this package is also compatible with the Sawyer research robot.

<center><h3>Table of Contents</h3></center>
<a href="#status">Current Status</a><br>
<a href="#hardware">Hardware</a><br>
<a href="#ps3_nodes">PS3 Controller Nodes</a><br>
<a href="#omni_nodes">Geomagic Touch Controller Nodes</a><br>
<a href="#ps3con">PS3 Controls</a><br>
<a href="#omnicon">Geomagic Touch Controls</a><br>
<a href="#launch">Launch Files</a><br>
<a href="#sources">Related Resources</a><br>

<center><h3 id="status">Current Status</h3></center>
<img src="img/portfolio/5/omnivc_demo.gif" class="img-responsive"><br>
The above GIF showcases how accurately the velocity controller is able to follow the target frame as the user moves the goal configuration with the Geomagic Touch's stylus.

<center><h3 id="hardware">Hardware</h3></center>
<b>Geomagic Touch</b> (formerly the Phantom Omni)<br>
The <a href="http://www.geomagic.com/en/products/phantom-omni/overview">Geomagic Touch</a> is a compact motorized device which can provide up to 3 degrees of freedom of force feedback in the x, y, and z direction.

<b>PS3 DUALSHOCK3 Controller</b>

<b>Rethink Robotics Baxter or Sawyer Robot</b><br>
Baxter and Sawyer are two robots developed by <a href="http://www.rethinkrobotics.com/">Rethink Robotics</a> which sport 7 degree of freedom anthropomorphic arms.

<center><h3 id="ps3_nodes">PS3 Controller Nodes</h3></center><br>
<b>joystick_reference_targets.py</b><br>
Subscribed topics: `joy`<br>
Published topics: `ref_pose`

This node uses the position of the PS3 sticks to create target end-effector poses. If the user attempts to drive the arm out of the defined workspace, the generated pose is clipped to the volume boundary. As a safety precaution, new configurations are only generated when the L1 button is pressed. This ensures that the arm will not move suddenly if the controller is bumped or dropped accidentally.

<b>velocity_control.py</b><br>
Subscribed topics: `ref_pose`<br>
Sawyer equivalent: `sawyer_velocity_control.py`

This node performs inverse kinematics to find a set of joint angle velocities which will allow Baxter's right arm to reach a particular position in space. It constantly monitors topic `ref_pose` to acquire the desired end-effector state. The script baxter_right_description.py provides the node with the home configuration and spatial screw axes of the right arm. These matrices are later used to derive the body Jacobian and twists for Baxter's current configuration using the formula below:

\begin{equation}
\Large
\nu_b = J_b(\theta)\dot{\theta}
\end{equation}

When the pose desired is unreachable or near a singularity, using the pseudoinverse of the Jacobian to find joint velocities may cause the system to become unstable. This is because the Jacobian only uses first-order expressions to approximate end-effector movements. One work around involves using the damped least-squares (DLS) inverse of the Jacobian to compute joint velocities.

\begin{equation}
\Large
\dot{\theta}= (J(\theta)^{T}J(\theta) + \lambda^{2}I)^{-1}J(\theta)^{T}\nu
\end{equation}

In the equation shown above, $$\dot{\theta}$$ is a matrix of joint velocities while lambda represents a damping parameter. In this node, the value of lambda (0.005) was found empirically.

<b>gripper_control.py</b><br>
Subscribed topics: `joy`<br>
Sawyer equivalent: `sawyer_gripper_control.py`

This node controls Baxter's right gripper when the L1 button is held down. It closes the robot's hand when the R1 button is pressed simultaneously.

<center><h3 id="omni_nodes">Geomagic Touch Controller Nodes</h3></center><br>
<b>omni_reference_targets2.py</b><br>
Subscribed topics: `/omni1_joint_states`<br>
Published topics: `/run_status`, `ref_pose`<br>

This node uses the transform between the Touch's stylus frame to its base frame to create target end-effector poses. It maps rotations about the Touch's third wrist joint to rotations about the target frame's z-axis using JointState messages read from topic `/omni1_joint_states`. If the user attempts to drive the arm out of the defined workspace, the generated pose is clipped to the volume boundary. As a safety precaution, new configurations are only generated when the 's' start key on the keyboard has been pressed.

<b>velocity_control.py</b><br>
The velocity control script used to control Baxter with the Touch is the same as the one used by the PS3 controller.

<b>omni_gripper_control.py</b><br>
Subscribed topics: `/run_status`, `omni1_button`<br>
This node controls Baxter's right gripper when the controller is enabled via the 's' start key. It closes the robot's hand when the white button on the Touch's stylus is held down.

<center><h3 id="ps3con">PS3 Controls</h3></center>

<img src="img/portfolio/5/ps3_controls.png" class="img-responsive">

~~~
L1 button : Hold down to enable robot movement
R1 button : Hold down to close robot end-effector
Left stick (L/R) : Horizontal movement along the Y-axis
Left stick (U/D) : Vertical movement along the Z-axis
Right stick (U/D) : Horizontal movement towards or away from user along the X-axis
Right stick (L/R) : Rotates the gripper clockwise or counterclockwise
~~~

<center><h3 id="launch">Launch Files</h3></center><br>
`simstate.launch` |
This file brings up an rviz simulation of Baxter as well as a GUI which enables users to manipulate and view individual joint angles.

`joysys.launch` |
This file simultaneously launches all of the nodes needed to run the joystick velocity control demonstration on Baxter. It pulls up an rviz simulation which shows the location of the goal end-effector pose and Baxter's movements as the arm chases down the target frame controlled by the user in real-time.

`sawyer_joysys.launch` |
This file performs the same actions as joysys.launch, except for Sawyer.

`omnisys.launch` |
This file simultaneously launches all of the nodes needed to run the Geomagic Touch velocity control demonstration on Baxter. It pulls up an rviz simulation which accurately displays where the Touch is positioned relative to Baxter in real life. It also streams the location of the goal end-effector pose and Baxter's movements as the user drives the target frame around in real-time.

<center><h3 id="sources">Related Resources</h3></center>
To download or read more about the Telehaptics ROS package, please head on over to the <a href="https://github.com/stephanniec/baxter_telehaptics">baxter_telehaptics</a> Github repository.
<br>
1. <a href="https://github.com/HuanWeng/ModernRobotics">ModernRobotics</a> Github repository
2. <a href="https://github.com/gt-ros-pkg/hrl-kdl">hrl-kdl</a> Github repository
3. S. Chiaverini, B. Siciliano, and O. Egeland, <a href="/files/leastsqrinvkin.pdf">Review of damped least-squares inverse kinematics with experiments on an industrial robot manipulator, IEEE Transactions on Control Systems Technology</a>, 2 (1994), pp. 123–134.
4. <a href="https://github.com/danepowell/phantom_omni">phantom_omni</a> Github repository
5. <a href="https://github.com/MurpheyLab/trep_omni">trep_omni</a> Github repository
