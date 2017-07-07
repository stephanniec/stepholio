---
title: PIC32 Control of a Brushed DC Motor
subtitle: Mechatronics
layout: default
modal-id: 4
date: 2017-03-19
thumbnail: pic32_motor_track.gif
alt: image-alt
project-date: March 2017
client: ME 333 Introduction to Mechatronics
category: Mechatronics
description:
---
<center><h3>Overview</h3></center>
PIC32 Control of a Brushed DC Motor was completed for the Introduction to Mechatronics course at Northwestern. For the final exam, students were asked to develop a smart motor driver which enables a brushed permanent magnet DC motor to track reference positions, velocities and torques.

A MATLAB client interface was created to relay user commands to an <a href="http://hades.mech.northwestern.edu/index.php/NU32#The_NU32">NU32 microcontroller board</a>. On the PIC32 chip, these commands were interpreted by C code which used 5 switch cases, a low-frequency PID position control loop, and a nested high-frequency PI current control loop to dictate motor behavior.   

<center><h3>The Five Motor Switch Cases</h3></center>
<b>IDLE</b><br>
In this mode, no voltage is sent to the motor.

<b>PWM</b><br>
In this mode, a user-defined PWM duty cycle sets the speed and direction of the motor.

<b>ITEST</b><br>
In this mode, the current controller's ability to track 2-4 cycles of a 100 Hz, 50% duty cycle, $$\pm{200}$$ mA square wave reference current is evaluated and plotted for PI gain tuning.

<b>HOLD</b><br>
In this mode, the motor moves to a user-defined position and attempts to maintain this configuration indefinitely.

<b>TRACK</b><br>
In this mode, the motor executes a desired trajectory specified by time points (in seconds) and motor positions (in degrees). As the shaft moves, readings measured by an encoder are stored and subsequently plotted for PID gain tuning.

<center><h3>Gain Tuning</h3></center>

<img src="img/portfolio/4/best_ITEST.png" class="img-responsive">
<center><b>Figure 1</b>: Evaluation of System's Ability to Replicate a 200mA Square Wave. Blue denotes the reference square wave, while red denotes the actual current measured across the motor.</center>
<br>
To regulate current, the best PI gains were found to be Kp = 45 mV/mA and Ki = 1.75 mV/mA. These values were determined from the test shown in <b>Figure 1</b>. Although some lag is present, the red curve exhibits minimal overshoot and successfully toggles between $$\pm{200}$$ mA.

<img src="img/portfolio/4/best_cubic.png" class="img-responsive">
<center><b>Figure 2</b>: Evaluation of System's Ability to Follow a Trajectory. Blue denotes the reference cubic wave, while red denotes the actual motor positions read by the encoder.</center>
<br>
To track position, the best PID gains were found to be Kp = -2.5 mA/deg, Ki = 0 mA/deg, and Kd = -100 mA/deg. These values were derived from the test shown in <b>Figure 2</b>. During testing, the motor was able to hit the correct angles roughly around the desired times. Minor overshoot occurred after 1.0s due to delayed changes in current. In hold mode, position recovery worked only when perturbations moved the inertial load bar less than 1080&deg; away from the reference angle.

<center><h3>Results</h3></center>
<div class="row">
  <div class="col-lg-2 col-md-1">
  </div>
  <div class="col-lg-8 col-md-10 col-sm-12">
    <div class="embed-responsive embed-responsive-16by9" style="center">
      <iframe class="embed-responsive-item" src="https://www.youtube.com/embed/GMUKL-pQ2tU?ecver=1" allowfullscreen></iframe>
    </div>
  </div>
  <div class="col-lg-2 col-md-1">
  </div>
</div>
<br>
This video shows how the motor behaves when a -100% duty cycle and a 100% duty cycle are sent to the PIC32 sequentially. During testing, the motor was able to reach its maximum speed within 5 seconds.

<div class="row">
  <div class="col-lg-2 col-md-1">
  </div>
  <div class="col-lg-8 col-md-10 col-sm-12">
    <div class="embed-responsive embed-responsive-16by9" style="center">
      <iframe class="embed-responsive-item" src="https://www.youtube.com/embed/YZxAcftRakI?ecver=1" allowfullscreen></iframe>
    </div>
  </div>
  <div class="col-lg-2 col-md-1">
  </div>
</div>
<br>
This video shows how the motor behaves when a cubic reference trajectory is sent to the PIC32. The test trajectory (0s, 0&deg; | 1.0s, 90&deg; | 1.5s -45&deg; | 2.5s, 0&deg;) is reproduced faithfully. When the bar ceases moving, the system clearly resists when I disturb the propeller away from its final configuration.

<center><h3>Related Resources</h3></center>
To download this software, please head on over to the <a href="https://github.com/stephanniec/pic32-DC-Motor-Controller">pic32-DC-Motor-Controller</a> Github repository.
