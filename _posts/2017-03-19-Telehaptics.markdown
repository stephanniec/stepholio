---
title: Haptic Feedback and Remote Control of a Robotic Arm
subtitle: Human-Machine Interaction
layout: default
modal-id: 5
date: 2017-03-19
thumbnail: telehapticstemp.png
alt: image-alt
project-date: January 2017- March 2017
client: Northwestern MSR
category: Human-Machine Interaction
description: An interface which allows human users to feel what robots feel
---
<center><h3>Overview</h3></center>
Haptic perception is an intrinsic facet of the somatosensory system which grants humans the ability to discern valuable information about the shape, orientation, and texture of objects in the world. Without it, even simple motor tasks can become frustratingly difficult to perform. The lack of tactile feedback in commercially-available prosthetics and teleoperated devices is a debilitating obstacle which prevents amputees, technicians and surgeons from moving naturally and dexterously with artificial limbs.

Telehaptics is a ROS Python package which brings to life a basic haptic interface using a Baxter research robot and the Geomagic Touch. When the stylus of a Touch is moved, Baxter's right arm will trace the same motions performed. If an external force is applied to the arm, the Touch will remotely apply the same forces to the user's hand. Together, these components form a closed-loop biofeedback system which enables users to experience something akin to telekinesis.

Note, this package is also compatible with the Sawyer research robot.

<center><h3>Current Status</h3></center>
<img src="img/portfolio/5/joyvc_demo.gif" class="center"><br>
The above gif showcases how well the velocity controller is able to chase the target frame as the user moves the goal configuration linearly in the x, y, and z directions and about the z-axis.

<center><h3>Hardware</h3></center>
<b>Geomagic Touch</b> (formerly the Phantom Omni)<br>
The <a href="http://www.geomagic.com/en/products/phantom-omni/overview">Geomagic Touch</a> is a compact motorized device which can provide up to 3 degrees of freedom of force feedback in the x, y, and z direction.

<b>PS3 Console</b>

<b>Baxter or Sawyer from Rethink Robotics</b>

<center><h3>Key Nodes</h3></center><br>
<b>joystick_reference_targets.py</b><br>
Subscribed topics: 'joy'<br>
Published topics: 'ref_pose'

This node uses the position of the PS3 sticks to create target end-effector poses. If the user attempts to drive the arm outside the defined workspace, the generated pose is clipped to the volume boundary. As a safety precaution, new configurations are only generated when the L1 button is pressed. This ensures that the arm will not move suddenly if the console is bumped accidentally.

<b>velocity_control.py</b><br>
Subscribed topics: 'ref_pose'<br>
Sawyer equivalent: sawyer_velocity_control.py

This node performs inverse kinematics to find a set of joint angle velocites which will allow Baxter's right arm to reach a particular position in space. It constantly monitors topic 'ref_pose' to acquire the desired end-effector state. The script baxter_right_description.py provides the node with the home configuration and spatial screw axes of the right arm. These matrices are later used to derive the body Jacobian and twists for Baxter's current configuration using the formula below:

<img src="img/portfolio/5/jacobiantwist.png" class="center">

Note, when the pose desired is unreachable or near a singularity, using the pseudoinverse of the Jacobian to find joint velocities may cause the system to become unstable. This is because the Jacobian only uses first-order expressions to approximate end-effector movements. One work around involves using the damped least-squares (DLS) inverse of the Jacobian to compute joint velocities.

<img src="img/portfolio/5/leastsqreqn.png" class="center">

In the equation shown above, q_dot is a matrix of joint velocities while lambda represents a damping parameter. In this node, the value of lambda (0.005) was found empirically.

<b>gripper_control.py</b><br>
Subscribed topics: 'joy'<br>
Sawyer equivalent: sawyer_gripper_control.py

This node controls Baxter's right gripper when the L1 button is held down. It closes the robot's hand when the R1 button is pressed.

<center><h3>Launch Files</h3></center><br>
<b>simstate.launch</b> |
This file brings up an rviz simulation of Baxter as well as a gui which enables users to manipulate and view individual joint angles.

<b>joysys.launch</b> |
This file simultaneously launches all of the nodes needed to run the joystick velocity control demonstration on Baxter. It pulls up an rviz simulation which shows the location of the goal end-effector pose and Baxter's movements as the arm chases down the target frame controlled by the user in real-time.

<b>sawyer_joysys.launch</b> |
This file performs the same actions as joysys.launch, except for Saywer.

<center><h3>Related Resources</h3></center>
To download or read more about the Telehaptics ROS package, please head on over to the <a href="https://github.com/stephanniec/baxter_telehaptics">baxter_telehaptics</a> Github repository.
<br>
1. <a href="https://github.com/HuanWeng/ModernRobotics">ModernRobotics</a> Github repository
2. <a href="https://github.com/gt-ros-pkg/hrl-kdl">hrl-kdl</a> Github repository
3. S. Chiaverini, B. Siciliano, and O. Egeland, <a href="/files/leastsqrinvkin.pdf">Review of damped least-squares inverse kinematics with experiments on an industrial robot manipulator, IEEE Transactions on Control Systems Technology</a>, 2 (1994), pp. 123–134.
4. <a href="https://github.com/MurpheyLab/trep_omni">Murphey Lab trep_omni</a> Github repository

