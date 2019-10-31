### Behavioral Cloning Project

This project is a part of:  
 [![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Main task of the project is to prepare model in [Keras](https://keras.io/) framework to drive a car inside simulator made by Udacity available in [this repo](https://github.com/udacity/self-driving-car-sim).
# Simulator

The simulator is not an app as I expected from the start.  
To run simulator it was needed to :
- Get [Unity framework](https://unity.com/) (Individual/Personal version was working fine)
- Use [git-lfs](https://help.github.com/en/github/managing-large-files/installing-git-large-file-storage) to get repository
- Fix deprecated code inside simulator [Assets/Standard Assets/Cameras/Scripts/TargetFieldOfView.cs](https://github.com/udacity/self-driving-car-sim/blob/master/Assets/Standard%20Assets/Cameras/Scripts/TargetFieldOfView.cs#L62) - 
```C#
if (!((r is TrailRenderer) || (r is ParticleRenderer) || (r is ParticleSystemRenderer)))
```

the "(r is ParticleRenderer)" check was deleted and  other stayed untouched so after change it stated:  

```C#
if (!((r is TrailRenderer) || (r is ParticleSystemRenderer)))
```

The simulator was ready to go:

![simulator](./images/simulator.png)

# Data Collection
I decided to collect drive data myself. It is qite challanging to drive car in the simulator - once you turn badly it gets even worse fast. After two learning circles I started recording.

Two recordings clock-wise and two counter-clock-wise were recorder as the data for training.

# Data Preprocessing

To cut off areas that should not affect the driving I calculated *'the mean frame'* of all recordings. Then Region Of Interest was marked.

![roi](./images/roi.png)

Data was normalized to range [-1;1]