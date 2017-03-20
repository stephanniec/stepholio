---
title: Haptics Feedback and Remote Control of Baxter
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

<center><h3>Hardware</h3></center>
<b>Geomagic Touch</b> (formerly the Phantom Omni)<br>
The <a href="http://www.geomagic.com/en/products/phantom-omni/overview">Geomagic Touch</a> is a compact motorized device which can provide up to 3 degrees of freedom of force feedback in the x, y, and z direction.

<center><h3>Node Network</h3></center><br>

<img src="img/portfolio/5/telehaptics_nodenetwork1.png" width="800" class="center">

<b>drawshape_ui.py</b><br>
Subscribed topics: 'give_move'<br>
Published topics: 'ui_output', 'sent_move'

This node continually publishes the poses of a hardcoded trajectory to commander.py. When a boolean flag read from topic 'give_move' is true, the script will send out a new pose. Conversely, if the flag is false, the node will continue to issue the same pose to topic 'ui_output'. In the final product, this node will function differently. It will convert the pose of the Touch's end-effector to a scaled set of equivalent coordinates in Baxter's workspace, before publishing the new desired pose to 'ui_output'.

<b>commander.py</b><br>
Subscribed topics: 'sent_move', 'ui_output', 'move_done'<br>
Published topics: 'target_position', 'start_move', 'give_move'

This node acts like the central nervous system of the Telehaptics package. When the program begins, it will first publish a home configuration to topic 'target_position'. Once Baxter's arm has returned home, the node will proceed to relay new Touch end-effector poses to the velocity controller in real-time.

<b>velcon.py</b><br>
Subscribed topics: 'start_move', '/robot/limb/right/endpoint_state', 'target_position'<br>
Published topics: 'robot/limb/right/joint_command', 'move_done'

This node performs inverse kinematics to find a set of joint angle velocites which will allow Baxter's right arm to reach a particular position in space. It constantly monitors topics 'target_position' and '/robot/limb/right/endpoint_state' to acquire the desired and current Baxter end-effector poses respectively. The script baxter_right_description.py provides the node with the home configuration and spatial screw axes of the right arm. These matrices are later used to derive the spatial Jacobian and twists for Baxter's current configuration - which can be related to angular velocity via the formula below:

<img src="img/portfolio/5/jacobiantwist.png" class="center">

Note, when the pose desired is unreachable or near a singularity, using the pseudoinverse of the Jacobian to find joint velocities may cause the system to become unstable. This is because the Jacobian only uses first-order expressions to approximate end-effector movements. One work around involves using the damped least-squares (DLS) inverse of the Jacobian to compute joint velocities.

<img src="img/portfolio/5/leastsqreqn.png" class="center">

In the equation shown above, q_dot is a matrix of joint velocities while lambda represents a damping parameter. Note, in this node, the value of lambda (0.005) was found empirically.

<center><h3>Launch Files</h3></center><br>
<b>simstate.launch</b> |
This file brings up an rviz simulation of Baxter as well as a gui which enables users to manipulate and view individual joint angles.

<b>telehaptics.launch</b> |
This file simultaneously launches all of the nodes needed to run the full Telehaptics package.

<center><h3>Related Resources</h3></center>
To download or read more about the Telehaptics ROS package, please head on over to the <a href="https://github.com/stephanniec/baxter_telehaptics">baxter_telehaptics</a> Github repository.
<br>
1. <a href="https://github.com/HuanWeng/ModernRobotics">ModernRobotics</a> Github repository
2. <a href="https://github.com/gt-ros-pkg/hrl-kdl">hrl-kdl</a> Github repository
3. S. Chiaverini, B. Siciliano, and O. Egeland, <a href="/files/leastsqrinvkin.pdf">Review of damped least-squares inverse kinematics with experiments on an industrial robot manipulator, IEEE Transactions on Control Systems Technology</a>, 2 (1994), pp. 123–134.
4. <a href="https://github.com/MurpheyLab/trep_omni">Murphey Lab trep_omni</a> Github repository

