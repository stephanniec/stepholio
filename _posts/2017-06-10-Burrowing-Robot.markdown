---
title: Burrowing Robot
subtitle: Prototyping
layout: default
modal-id: 7
date: 2017-06-10
thumbnail: burrowing_robot_icon.png
alt: image-alt
project-date: March 2017 - December 2017
client: Northwestern Department of Mechanical Engineering
category: Prototyping
description: Exploring New Mechanisms for Moving Underground
---
<center><h3>Overview</h3></center>
Subterranean navigation and operation is important for a sundry of tasks, such as mining, construction, reconnaissance and bomb detection. Although there are numerous robots available for working beneath snow and hard earth, fewer options exist for exploring spaces beneath granular media. To address this disparity, the burrowing robot project investigates how helical motion can be used to help robots "fly" within sand.

<center><h3>Table of Contents</h3></center>
<a href="#auger_proto">I. The Augerbot Prototype</a><br>
<a href="#auger_eval">II. Augerbot Performance Evaluations</a><br>
<a href="#cite">III. Acknowledgements</a>

<center><h3 id="auger_proto">The Augerbot Prototype</h3></center>
<img class="img-responsive" src="img/portfolio/7/screw_head_plane.png" width="600">
This prototype consists of 5 main components. When powered, an Archimedes screw mounted at the head of the robot will spin to part granular media and pull the robot forward. This is attached to an adapter plate which fits snugly around the shaft of a DC motor. A cylindrical cap on the motor itself stops granules from falling into an exposed gear box. Wedged inside the protective cap are wings which prevent the body of the robot from rotating with the screw. Lastly, an elongated hemisphere housing unit covers the back of the robot to shield soldered wire junctions from wear and tear. Note, a modular robot was created to make testing different combinations of screws and wing shapes easier.

<center><h3 id="auger_eval">Augerbot Performance Evaluations</h3></center>
<h4>TRIAL I</h4>
`Date:` June 11, 2017 <br>
`Task:` Test different wing and helix pitch permutations <br>
`Tests:` <br>
I. Submerged swimming (I) - Robot starts inside the poppy seed bed with its wings parallel to the bottom of the tank <br>
II. Surface swimming (II) - Robot starts on top of the poppy seed bed with its wings parallel to the bottom of the tank <br>
III. Burrowing (III) - Robot starts upside down with the screw head pointed at the surface of the poppy seed bed <br>
`Goal:` To empirically find the range of wing and helix parameters which will allow the robot to move consistently through the poppy seeds in 1D

<b>Testing Ground</b><br>
For prototyping, a tank of poppy seeds was used. Poppy seeds were chosen because the granules are roughly uniform in size. Before each test, the bed was fluidized to ensure even packing throughout the media. Below is a GIF of the bed being fluidized.

<img class="img-responsive" src="img/portfolio/7/fluidize.gif">

<b>Wings Tested</b><br>
Three sets of wings were created for trial 1. Their dimensions and shapes were arbitrarily selected.

<img class="img-responsive" src="img/portfolio/7/wings.png" width="600">
* Isoceles Triangle PLA 38.9mm long
* Rectangle PLA 44.6mm long
* Curved PLA 44.4mm long

<br><b>Auger Heads Tested</b><br>
Three auger heads were assembled for trial 1. Their lengths and pitch angles were randomly chosen.

<img class="img-responsive" src="img/portfolio/7/screws.png" width="600">
* 2-turns PLA 58.67mm long
* 3-turns PLA 58.67mm long
* 4-turns PLA 58.67mm long <br>

<br><b>Observations</b><br>
`Alpha 1.0` | Iso triangle wings | 3-loop screw <br>
<br>
I. Robot was unable to travel linearly. It would simply rotate in the horizontal plane, tilt up (about the axis its wings lie on) and resurface.

II. Robot spun in place in the horizontal plane. Did not travel linearly.

III. Robot was able to submerge itself but would quickly resurface.

`Alpha 1.1` | Rectangle wings | 3-loop screw <br>
<br>
I. Robot was unable to travel linearly. It simply would rotate, then resurface at a rate faster than Alpha 1.0.

II. Robot stayed in place, but rotated in the horizontal plane much more than Alpha 1.0.

III. Robot was able to submerge itself. Resurfaced much faster than Alpha 1.0.

`Alpha 1.2` | Curved wings | 3-loop screw <br>
<br>
I. Robot was unable to travel linearly. It simply would rotate, then resurface. Of all the submerged swimming tests conducted, however, this robot stayed under the longest.

II. Robot stayed in place, but rotated in the horizontal plane to a lesser degree than Alpha 1.1.

III. Robot was able to submerge itself completely. It briefly exhibited the ability to translate horizontally but would eventually resurface. Stayed under the seeds for a significantly longer period of time than the other prototypes.

<img class="img-responsive" src="img/portfolio/7/alpha_1p2_move.gif">

<b>Conclusions</b>
1. Curved wings performed the best
  * Triangle wings unable to resist torque
  * Rectangle wings create too much drag
2. Robot is bottom-heavy
  * Balance problem gradually causes it to tip up
3. Center of mass (COM) of robot is below the wings
  * Originally wanted COM to be between wings like in planes
4. Orienting the wings horizontally rather than vertically improves the robot's ability to move forward

<br><b>Future Direction</b>
1. Weigh down the front end of the robot
  * Use washers
  * Change screw material (e.g. metal)
2. Change power supply
  * Existing supply (12V, 8.4A) is not variable
3. Add universal hinge and counter weight to allow the robot to dive
  * Might be easier to adjust counter weight size to adjust COM position instead of messing with screw features

<center><h3 id="cite">Acknowledgements</h3></center>
<a href="http://www.mccormick.northwestern.edu/research-faculty/directory/affiliated/umbanhowar-paul.html">Dr. Paul Umbanhowar</a><br>
<a href="https://github.com/dlynch7">Dan Lynch</a>
