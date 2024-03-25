<p align="center">
<img src="/figures/RC_car_2_phones.jpg" alt="RC Car" width="500">
</p>

# MoRPI: Mobile Robot Pure Inertial Navigation

## Introduction

Mobile robots are used in industrial, leisure, and military applications.  In some situations, a robot navigation solution relies only on inertial sensors 
and as a consequence, the navigation solution drifts in time.
We propose the MoRPI framework, a mobile robot pure inertial approach. Instead of travelling in a straight line trajectory, the robot moves 
in a periodic motion trajectory to enable peak-to-peak estimation. In this manner, instead of performing three integrations to calculate the robot position 
in a classical inertial solution, an empirical formula is used to estimate the travelled distance. Two types of MoRPI approaches are suggested, where one is 
based on both accelerometer and gyroscope readings while the other is only on gyroscopes. Closed form analytical solutions are derived to show that MoRPI 
produces lower position error compared to the classical pure inertial solution. In addition, to evaluate the proposed approach, field experiments were made 
with a mobile robot equipped with two types of inertial sensors. In total, 143 trajectories with a time duration of 75 minutes were collected and evaluated. 
The results show the benefits of using our approach. 

## Dataset

A remote control car and a smartphone were used to perform the experiments and record the inertial data to create our dataset. The smartphone was rigidly 
attached to the car. The model of the RC car we used is a STORM Electric 4WD Climbing car. The car dimensions are 385x260x205mm with a wheelbase of 253mm 
and tire diameter of 110mm. The car has a realistic suspension system that enables it to reach up to 40 kph and cross rough terrain.
Two different smartphones, with different inertial sensors, were used in our experiments: 
  1. A Samsung Galaxy S8 Smartphone with an IMU model of LSM6DSL manufactured by STMicroelectronics. 
  2. A Samsung Galaxy S6 smartphone with an IMU model of MPU-6500 manufactured by TDK InvenSense.
In both smartphones, the inertial sensor readings were recorded with a sampling rate of 100Hz.

Five types of trajectories were made during the field experiments: Straight Line, Periodic Motion - Short Route, Periodic Motion - Long Route, L-Shaped - Straight Lines
and L-Shaped - Periodic Motion.
One hundred and three experiments were made indoors on a floor, while 40 experiments were recorded outdoors on an asphalt surface. The dataset of the periodic 
movement was split to have a variety of velocities in both train and test sets, where the train was used to determine the gain, and the test to examine our method. 
The groups were divided almost equally.

## Algorithm

<img alt="MoRPI Scheme" src="/figures/MoRPI_scheme.jpg" width="400">

Both of Our MoRPI approaches consist of the following phases:
  1. **Peak detection**: The peaks during the motion are extracted as local maxima from the inertial measurements.
  2. **Gain calculation**: Prior to the application of the proposed approach, the empirical gain is estimated by moving the robot at a known distance with a known 
     number of periods while using the Weinberg approach. Once obtained, this gain is used in real-time to estimate the peak-to-peak distance.
  3. **Peak-to-peak distance estimation**: The 'step', in analogue to PDR, is the segment between two peaks. The peak-to-peak distance estimation is done using the 
     Weinberg approach with the predefined gain and the inertial sensor readings.
  4. **Heading determination**: We use the heading extracted from the transfer matrix to project the peak-to-peak distance into local planar coordinates.
  5. **Position update**: As a dead-reckoning method, the position is updated relative to the previous step while using the current heading angle and peak-to-peak 
     distance.
      
 ## Citation
 
 If you found the experimental DATA useful or used our algorithm for your research, please cite our paper:
 ```
 @article{etzion2022morpi,
  title={MoRPI: Mobile Robot Pure Inertial Navigation},
  author = {Etzion, Aviad and Klein, Itzik},
  journal={IEEE Journal of Indoor and Seamless Positioning and Navigation},
  url = {https://ieeexplore.ieee.org/document/10323471},
  year={2022},
}
 ```
 
 [<img src=https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/ArXiv_web.svg/250px-ArXiv_web.svg.png width=70/>](https://arxiv.org/abs/2207.02982)
 
<p align="center">
<img src="https://github.com/ansfl/MEMS-IMU-Denoising/blob/main/figrues/Logo.png?raw=true" width="500" class="center"/>
</p>

