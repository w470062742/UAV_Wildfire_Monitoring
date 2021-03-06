# UAV Wildfire Monitoring

This repository presents animations (and in the future, code) to support the paper [Image-based Guidance of Autonomous Aircraft for Wildfire Surveillance and Prediction](https://arxiv.org/abs/1810.02455).

## Modeling
We use a simple stochastic wildfire model that divides an area of land into small cells with some amount of fuel. Each cell is burning or non-burning, and burning cells consume fuel until all the fuel is used and the cell extinguishes. Burning cells may ignite neighboring cells, and wind is modeled by increasing the likelihood that fire spreads in a given direction. The animation below demonstrates the wildfire model.

![Wildfire Simulation](https://github.com/sisl/UAV_Wildfire_Monitoring/blob/master/animations/Wildfire.gif)

The goal of this work is to develop a controller to guide an aircraft to image a wildfire and monitor its growth. Trajectories can be parameterized by changing the aircraft bank angle by 5 deg at a frequency of 10 Hz. This work models an aircraft with four cameras, and the region being imaged rotates as the aircraft bank angle changes. The camera images are imperfect, so 10% of observations are randomly changed, and the sensing range of the cameras is limited to 300 m. The animation below shows the imaging regions as the aircraft banks in different directions.

![Aircraft Simulation](https://github.com/sisl/UAV_Wildfire_Monitoring/blob/master/animations/Sensors.gif)

## Approach

We want to use the noisy images to guide the aircraft. One way to do this is to filter and combine the images into a large belief map of wildfire locations, which allows previous observations to be preserved. We present to methods to filter the images and create the belief map: an extended Kalman filter (EKF) approach and a partilce filter (PF) approach. The belief maps are used as inputs to a neural network controller trained through simulation using deep Q-learning.

## EKF
The animation below shows two aircraft flying with the trained controller which uses an EKF to create the belief map.
![EKF Simulation](https://github.com/sisl/UAV_Wildfire_Monitoring/blob/master/animations/EKF.gif)

## PF
The animation below shows two aircraft flying with the trained controller which uses a particle filter to create the belief map.
![PF Simulation](https://github.com/sisl/UAV_Wildfire_Monitoring/blob/master/animations/PF.gif)
