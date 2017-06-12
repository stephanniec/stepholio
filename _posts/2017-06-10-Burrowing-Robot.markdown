---
title: Burrowing Robot
subtitle: Mechatronics
layout: default
modal-id: 7
date: 2017-06-10
thumbnail:
alt: image-alt
project-date: March 2017 - December 2017
client: Northwestern Department of Mechanical Engineering
category: Mechatronics
description: Exploring New Mechanisms for Moving Underground
---
<center><h3>Overview</h3></center>
Subterranean robotic navigation and operation is important to a sundry of industries. Aside from mining, construction and reconnaissance, more and more autonomous robots are being deployed by the military to remotely locate and detonate explosive devices. Although there are numerous robots available for working beneath snow and hard earth, less options exist for exploring spaces beneath granular media. To address this disparity, the burrowing robot project was launched to develop new methods for allowing robots to "fly" within sand.

<center><h3>Screw-Head Plane Prototype</h3></center>
<img src= "img/portfolio/7/screw_head_plane.png" width="600" class="img-responsive">
This prototype consists of 5 main components. Starting from the left to the right, an Archimedes screw mounted at the head of the robot will spin to part granular media and pull the robot forward. This is attached to an adapter plate which fits snugly around a DC motor shaft. A cylindrical cap on the motor itself prevents granules for falling into the exposed gear box. Wedged inside the protective cap are the wings which will prevent the entire body of the robot from rotating with the screw head. Lastly, an elongated hemisphere housing unit encloses the wire leads.

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
`Testing ground:` Poppy seed bed<br>
`Tests`: Submerged swimming (I), Surface swimming (II), Burrowing (III) <br>
`Goal:` To design and create a plane-like prototype which allows the robot to move consistently through the poppy seeds

<b>Alpha 1.0</b><br>
Iso triangle wings | 3-loop screw
I.

II.

III.

<b>Alpha 1.1</b><br>
Rectangle wings | 3-loop screw
I.

II.

III. Robot was able to submerge itself. Resurfaced much faster than Alpha 1.0.

<b>Alpha 1.2</b><br>
Curved wings | 3-loop screw
I.

II.

III. Robot was able to submerge itself

<b>Conclusions</b>
* Curved wings performed the best
* Balance problem causes robot to tip up
* Center of mass of robot is below the wings
* Orienting the wings horizontally improves ability to move forward
* Motor does not have enough power to propel robot forward
  * Motor has enough torque - does not stall
  * Motor does not spin fast enough - already using max rated voltage

<b>Future Direction</b>
* Weigh down the front end of the robot
  * Use washers
  * Change screw material (e.g. metal)
* Change power supply - existing supply (12V, 8.4A) is not variable

<center><h3>Acknowledgements</h3></center>
<a href="http://www.mccormick.northwestern.edu/research-faculty/directory/affiliated/umbanhowar-paul.html">Dr. Paul Umbanhowar</a>
<a href="https://github.com/dlynch7">Dan Lynch</a>
