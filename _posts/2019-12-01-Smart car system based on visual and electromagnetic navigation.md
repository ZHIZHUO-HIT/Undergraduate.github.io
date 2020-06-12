---
title: Smart car system based on visual and electromagnetic navigation
layout: post
img: shuangche.jpg
categories: ''
tags: ''
---
## Introduce
Designed two cars with electromagnetic sensors, cameras, speed encoders, ultrasonic sensors, laser sensors, gyro accelerometers to finish the closed circuit.  The track is white, the background is blue, and there is a  alternating current line in the middle of the track. There are complex elements in the track such as: intersections, roundabouts, s-curves etc. 

## Project source

This source is from College Student Smart Car Competition  sponsored by NXP. I have participated in this competition with two teammates twice, each season lasted for eight months.

## Some photos and videos

Video of  heat:

此处插入省赛视频

Video of  final:

此处插入国赛视频

Several versions of the car :

![1]({{site.baseurl}}/assets/img/a.jpg)

![2]({{site.baseurl}}/assets/img/b.jpg)

![3]({{site.baseurl}}/assets/img/c.jpg)

## Navigation algorithm

### (1)  Navigation algorithm based on camera

OV7725 CMOS camera was used to achieve the fast extraction of the track centre line. The process is mainly divided into the following steps.

- Binarize the image

  The original image and the binarized image are as follows:

​       ![4]({{site.baseurl}}/assets/img/d.PNG)

- Extract the edges of the track

  We used an eight-point neighborhood algorithm, the edge of the track can be  calibration in the image as shown below:

  ![5]({{site.baseurl}}/assets/img/e.png)

- Correct the image

  Due to the distortion of the camera image, barrel transformation and perspective transformation of the image are required. The comparison image of the simulated correction is as follows:

  ![6]({{site.baseurl}}/assets/img/f.jpg)

- Calculate the track centerline

  The center line of the track is the expected trajectory of the car, which requires different treatments for different elements, as well needs the trajectory prediction for blind spots. The centerline calculated can be shown below:

  ![7]({{site.baseurl}}/assets/img/g.png)

- Optimize the path

  The final score is closely related to the speed and path of the car, so the path needs to be optimized. For example, in the small s bend, go straight as far as possible, and drive at right angles to the inside.

### (2) Navigation algorithm based on wire guidance

A magnetic field is generated around the AC wire, and the LC oscillation circuit is used to detect the strength of the magnetic field, thereby extracting the track centerline. The process is mainly divided into the following steps.

- Sensor selection and installation

  Use seven pairs of inductance and capacitance in parallel, and then through the amplifier circuit and detection circuit. The circuit schematic and the sensor layout are shown below:

  ![8]({{site.baseurl}}/assets/img/h.PNG)

  ![9]({{site.baseurl}}/assets/img/i.PNG)

- Judging direction and special elements

  The data of horizontal inductance and vertical inductance can be merged to determine left turn and right turn. According to the middle inductance and diagonal inductance, special elements can be effectively determined.

- Sensor position solution

  Use the difference-ratio-sum algorithm to find the position of the sensor relative to the centerline initially. Because the magnetic field is distributed in a ring, this distance is not accurate.

- Find the exact position of the centerline

  Perform quadratic curve fitting on the sensor data to compensate the error of the magnetic field distribution. Obtain an accurate error between the center of the body and the centerline, which can be used for control system input.

## Control algorithm

### (1)  Steering servo control

The car uses a steering servo to turn, the actual picture is shown below:

![10]({{site.baseurl}}/assets/img/j.PNG)

We have try these control methods and applied them in MCU. Because the servo has a built-in encoder, the controller does not need the parameter D:

- PI controller
- PI controller with variable parameters 
- PI controller with integral separation
- Fuzzy PI controller
- The controller calculated from Ackerman corner model 

### (2)  Dual motor control

The car has two motors, each of them has independent controller, We have try these control methods and applied them in MCU.

- PID controller
- PID controller with integral separation
- Fuzzy PID controller
- Bang-bang controller
- Cascade PID controller

## Circuit design

The circuit boards on cars were designed by myself, including  MCU system board, motor drive board, sensors drive board etc. Some of them are shown below:

![14]({{site.baseurl}}/assets/img/p.jpg)

## Summary

We have won First Prize of 13th National College Student Smart Car Competition.

![11]({{site.baseurl}}/assets/img/m.jpg)

 I will never forget the experience of participating in this competition. From this competition I have consolidated knowledge learned from books, as well mastered how to solve practical engineering problems. In addition, I understand that cooperation is very important. I spend all my spare time on doing experiments with my two teammates in the lab, sometimes we even slept there.

![12]({{site.baseurl}}/assets/img/k.jpg)

![13]({{site.baseurl}}/assets/img/l.jpg)

Since then I always believe that **nothing is impossible. Your life is controlled by yourself.**





