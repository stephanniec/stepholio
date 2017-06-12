---
title: Burrowing Robot
subtitle: Mechatronics
layout: default
modal-id: 7
date: 2017-06-10
thumbnail: burrowing_robot_icon.png
alt: image-alt
project-date: March 2017 - December 2017
client: Northwestern Department of Mechanical Engineering
category: Mechatronics
description: Exploring New Mechanisms for Moving Underground
---
<center><h3>Overview</h3></center>
Subterranean robotic navigation and operation is important to a sundry of tasks, such as mining, construction, reconnaissance and bomb detection. Although there are numerous robots available for working beneath snow and hard earth, less options exist for exploring spaces beneath granular media. To address this disparity, the burrowing robot project was launched to discover new methods for allowing robots to "fly" within sand.

<center><h3>Screw-Head Plane Prototype</h3></center>
<img src= "img/portfolio/7/screw_head_plane.png" width="600" class="img-responsive">
This prototype consists of 5 main components. When powered, an Archimedes screw mounted at the head of the robot will spin to part granular media and pull the robot forward. This is attached to an adapter plate which fits snugly around a DC motor shaft. A cylindrical cap on the motor itself prevents granules from falling into the exposed gear box. Wedged inside the protective cap are wings which will prevent the body of the robot from rotating with the screw. Lastly, an elongated hemisphere housing unit covers the back of the robot to shield the soldered wire junctions from wear and tear.

<center><h4>Wings</h4></center>
<img src= "img/portfolio/7/wings.png" width="600" class="img-responsive">
* Isoceles Triangle PLA 38.9mm
* Rectangle PLA 44.6mm
* Curved PLA 44.4mm

<center><h4>Screw Heads</h4></center>
<img src= "img/portfolio/7/screws.png" width="600" class="img-responsive">
* 2-loop PLA 58.67mm
* 3-loop PLA 58.67mm
* 4-loop PLA 58.67mm

<center><h3>Screw-Head Prototype Performance</h3></center>
<b>TRIAL I</b><br>
`Objective:` Test different wing and screw pitch permutations<br>
`Tests`: Submerged swimming (I), Surface swimming (II), Burrowing (III) <br>
`Goal:` To design and create a plane-like prototype which allows the robot to move consistently through the poppy seeds in 1D

<b>Testing Ground</b><br>
For prototyping, a tank of poppy seeds was used. Poppy seeds were chosen because the granules are roughly uniform in size. Before each test, the bed was fluidized to ensure even packing throughout the media. Below is a GIF of the bed being fluidized.

<img src="img/portfolio/7/fluidize.gif" class="img-responsive">

<b>Alpha 1.0</b><br>
Iso triangle wings | 3-loop screw<br>
<br>
I. Robot was unable to travel linearly. It simply would rotate about the z-axis, then tilt up about the x-axis and resurface.

II. Robot simply spun in place. Did not travel linearly nor rotate.

III. Robot was able to submerge itself but would quickly resurface.

<b>Alpha 1.1</b><br>
Rectangle wings | 3-loop screw<br>
<br>
I. Robot was unable to travel linearly. It simply would rotate, then resurface at a rate faster than Alpha 1.0.

II. Robot stayed in place but rotated about the z-axis significantly.

III. Robot was able to submerge itself. Resurfaced much faster than Alpha 1.0.

<b>Alpha 1.2</b><br>
Curved wings | 3-loop screw<br>
<br>
I. Robot was unable to travel linearly. It simply would rotate, then resurface. Of all the submerged swimming tests conducted, however, this robot was able to stay underground the longest.

II. Robot stayed in place and rotated, but to a lesser degree than Alpha 1.1.

III. Robot was able to submerge itself completely. It briefly exhibited the ability to translate in the xy-plane but would eventually resurface. Stayed under the seeds for a significantly longer period of time than the other prototypes.

<img src="img/portfolio/7/alpha_1p2_move.gif" class="img-responsive">

<b>Conclusions</b>
<ol>
<li>Curved wings performed the best</li>
  <ul>
  <li>Triangle wings unable to resist torque</li>
  <li>Rectangle wings create too much drag</li>
  </ul>
<li>Balance problem causes robot to tip up</li>
<li>Center of mass of robot is below the wings</li>
<li>Orienting the wings horizontally improves ability to move forward</li>
<li>Motor does not have enough power to propel robot forward</li>
  <ul>
  <li> Motor has enough torque - does not stall</li>
  <li> Motor does not spin fast enough - already using max rated voltage</li>
  </ul>
</ol><br>

<b>Future Direction</b>
1. Weigh down the front end of the robot
  * Use washers
  * Change screw material (e.g. metal)
2. Change power supply - existing supply (12V, 8.4A) is not variable

<center><h3>Acknowledgements</h3></center>
<a href="http://www.mccormick.northwestern.edu/research-faculty/directory/affiliated/umbanhowar-paul.html">Dr. Paul Umbanhowar</a><br>
<a href="https://github.com/dlynch7">Dan Lynch</a>
