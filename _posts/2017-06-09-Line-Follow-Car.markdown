---
title: Line Following Robot
subtitle: Mechatronics
layout: default
modal-id: 6
date: 2017-06-10
thumbnail: line_follow_car.gif
alt: image-alt
project-date: March 2017 - June 2017
client: ME 433 Advanced Mechatronics
category: Mechatronics
description:
---
<center><h3>Overview</h3></center>

<center><h3>The Map</h3></center>
<img src= "img/portfolio/6/techcup2017.png" width="600" class="img-responsive">

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

<center><h3>Hardware</h3></center>

<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
.slidesMod6 {margin:0 auto;}
</style>

<div class="slide-content w3-display-container" style="max-width:800px">
  <img class="slidesMod6 img-responsive" src= "img/portfolio/6/line_follow_car.png">
  <img class="slidesMod6 img-responsive" src= "img/portfolio/6/car_cad.png">
  <img class="slidesMod6 img-responsive" src= "img/portfolio/6/4in_wheel_cad.png">
  <img class="slidesMod6 img-responsive" src= "img/portfolio/6/motor_bracket_cad.png">
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
  var x = document.getElementsByClassName("slidesMod6");
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
</script>

<center><h3>Related Resources</h3></center>
To download or read more about the Line Following Robot and other small mechatronics projects, please head on over to the <a href="https://github.com/stephanniec/stephanniec_ME433_2017">stephanniec_ME433_2017</a> Github repository.
