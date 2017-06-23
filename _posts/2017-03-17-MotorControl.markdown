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
PIC32 Control of a Brushed DC Motor is a project which was completed for the Introduction to Mechatronics course at Northwestern. For the final exam, students were asked to develop a smart motor driver which uses feedback control to enable a brushed permanent magnet DC motor to track reference positions, velocities and torques.

A MATLAB client interface was created to convey user commands to an <a href="http://hades.mech.northwestern.edu/index.php/NU32#The_NU32">NU32 microcontroller board</a>. On the PIC32 chip, these commands are interpreted by C code which uses 5 switch cases, a low-frequency PID position control loop, and a nested high-frequency PI current control loop to dictate motor behavior.   

<center><h3>Motor Modes</h3></center>
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

<center><h3>Results</h3></center>


<center><h3>Related Resources</h3></center>
To download this software, please head on over to the <a href="https://github.com/stephanniec/pic32-DC-Motor-Controller">pic32-DC-Motor-Controller</a> Github repository.
