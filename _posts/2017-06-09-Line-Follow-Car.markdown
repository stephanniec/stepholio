---
title: Line Following Robot
subtitle: Prototyping - Mechatronics
layout: default
modal-id: 6
date: 2017-06-10
thumbnail: line_follow_car.gif
alt: image-alt
project-date: March 2017 - June 2017
client: ME 433 Advanced Mechatronics
category: Prototyping - Mechatronics
description:
---
<center><h3>Overview</h3></center>
The Line Following Robot was built for the 2017 Tech Cup at Northwestern. It uses an Android application coupled with a custom PIC32 PCB to steer a differential drive vehicle around a gray racetrack. Information is transfered between the application and the microcontroller via USB communication. Aside from sending velocity commands, the phone also provides power to two N20 brushed DC gearhead motors.

<center><h3>The Map</h3></center>
<img class="img-responsive" src="img/portfolio/7/techcup2017.png" width="600">
This is the course that the robots competed on. Although it is not shown, a 12" wide x 12" tall plywood gate served as both the start and finish line.

<center><h3>Motor Control</h3></center>  
<div class="row">
  <div class="col-lg-2 col-md-1">
  </div>
  <div class="col-lg-8 col-md-10 col-sm-12">
    <div class="embed-responsive embed-responsive-16by9" style="center">
      <iframe class="embed-responsive-item" src="https://www.youtube.com/embed/R9pwJjqRXbo?ecver=1" allowfullscreen></iframe>
    </div>
  </div>
  <div class="col-lg-2 col-md-1">
  </div>
</div>
<br>
This is a video of some preliminary motor control tests I performed using two 4-inch wheels I designed in OnShape and 3D printed in PLA. Outside the view of the camera, I am periodically sending new slider bar and switch values from a rudimentary Android application control panel to the PIC32. On the microcontroller, the slider positions are converted to PWM duty cycle percentages. The switch positions, on the other hand, are used to toggle boolean flags that dictate whether the voltage applied to the motors should be positive or negative.

<center><h3>Path Detection</h3></center>
<div class="row">
  <div class="col-lg-2 col-md-1">
  </div>
  <div class="col-lg-8 col-md-10 col-sm-12">
    <div class="embed-responsive embed-responsive-16by9" style="center">
      <iframe src="https://www.youtube.com/embed/wmvf4Z9TsZw?ecver=1" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
  <div class="col-lg-2 col-md-1">
  </div>
</div>
<br>
This video shows the racetrack centerline locater working as I walk around the map. The black lines indicate where the software believes a gray path exists. The red dots mark where the midpoint of each black line is.

<center><h3>Hardware</h3></center>
<style>
.mySlidesCar {margin:0 auto;}
</style>

<div class="slide-content" style="max-width:800px">
  <img class="mySlidesCar img-responsive" src="img/portfolio/7/line_follow_car.png">
  <img class="mySlidesCar img-responsive" src="img/portfolio/7/car_cad.png">
  <img class="mySlidesCar img-responsive" src="img/portfolio/7/4in_wheel_cad.png">
  <img class="mySlidesCar img-responsive" src="img/portfolio/7/motor_bracket_cad.png">
</div>

<center>
  <button type="button" class="btn btn-primary" onclick="divNow(1)">The Robot</button>
  <button type="button" class="btn btn-primary" onclick="divNow(2)">Car Chassis</button>
  <button type="button" class="btn btn-primary" onclick="divNow(3)">Wheels</button>
  <button type="button" class="btn btn-primary" onclick="divNow(4)">Motor Brackets</button>
</center>

<script>
var ind = 1;
slideshow(ind);

function divAdd(n) {
  slideshow(ind += n);
}

function divNow(n) {
  slideshow(ind = n);
}

function slideshow(n) {
  var i = 0;
  var x = document.getElementsByClassName("mySlidesCar");
  var dots = document.getElementsByClassName("btn-primary");
  if (n > x.length) {ind = 1}
  if (n < 1) {ind = x.length}
  for (i = 0; i < x.length; i++) {
     x[i].style.display = "none";
  }
  for (i = 0; i < dots.length; i++) {
     dots[i].className = dots[i].className.replace("btn btn-secondary", "");
  }
  x[ind-1].style.display = "block";
  dots[ind-1].className += "btn btn-primary";
}
</script><br>

<center><h3>Results</h3></center>
<div class="row">
  <div class="col-lg-2 col-md-1">
  </div>
  <div class="col-lg-8 col-md-10 col-sm-12">
    <div class="embed-responsive embed-responsive-16by9" style="center">
      <iframe src="https://www.youtube.com/embed/88SlMiolcFQ?ecver=1" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
  <div class="col-lg-2 col-md-1">
  </div>
</div>
<br>
<b>Overcoming Inertia</b><br>
During testing, the robot would only forward when duty cycles greater than 75% were used. As a result, the car would either shoot off the road too quickly for the path recovery algorithm to find the racetrack, or not move at all. To generate higher torque at lower motor velocities, 2-inch wheels (instead of the original 4-inch ones) were used in the final design.  

<b>Lighting</b><br>
The images captured by the rear phone camera sometimes looked strangely yellow. This primarily occurred whenever the car would move from a patch of shade to a sunlit region. If the transition happened during a turn, the image processing algorithm would incorrectly identify the racetrack's location. To remedy this, only the bottom third of the camera feed was analyzed to give the phone more time to adjust to ambient light changes. OpenCV also should have been used to raise the application's frame rate.

<center><h3>Related Resources</h3></center>
To download or read more about the Line Following Robot and other small mechatronics projects, please head on over to the <a href="https://github.com/stephanniec/stephanniec_ME433_2017">stephanniec_ME433_2017</a> Github repository.
