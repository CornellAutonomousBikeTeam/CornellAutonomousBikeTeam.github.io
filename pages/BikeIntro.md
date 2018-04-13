# A Gentle Introduction to the Bike

# Basic Parts of the Bike

This is MIKE (Mechanical Irritating Kickstand Experiment) the bike:
[[/img/bike.png | alt = bike]]

The goal of this bike to be the world's first self-steering, self-balancing, and self-navigating bicycle. So let's get down to the basic parts of the bike:

## Battery


[[https://github.com/CornellAutonomousBikeTeam/CornellAutonomousBikeTeam.github.io/blob/master/img/battery.jpg | alt = battery]]

This is our battery. Our batteries have a nominal voltage of 27 V, which means
that their voltage can range from 25-29 V. In order to run on the bike, you want
the voltage to be at least ** V. If it's not, there's a charger underneath the
Record-Breaking Walking Robot - just remember to unplug the battery if you
leave the lab or if the battery finishes charging, otherwise you are at risk of damaging the battery and this will make your team lead angry. :(

## IMU

![IMU]
(https://github.com/CornellAutonomousBikeTeam/CornellAutonomousBikeTeam.github.io/blob/master/img/imu.jpg)

This is the IMU, which stands for inertial measurement unit. The IMU has several features, including accelerometers, gyroscopes, and magnemometers, and uses these to measure a variety of data, including force, angular rate, magnetic fields, and Euler angles.

### A brief interlude about Euler Angles
[insert image of Euler angles here]

There are three directions Euler angles measure: roll, pitch, and yaw.

## Raspberry Pi

![Raspberry pi]
(https://github.com/CornellAutonomousBikeTeam/CornellAutonomousBikeTeam.github.io/blob/master/img/pi.jpg)

This is the raspberry pi. A Raspberry Pi is essential a tiny single-board computer. 

## PCB

![PCB]
(https://github.com/CornellAutonomousBikeTeam/CornellAutonomousBikeTeam.github.io/blob/master/img/pcb.jpg)

This is our printed circuit board. The Cornell Autonomous Bike Team and CU Sail
collaborated to specially design this board so that both teams could use it as
we have many similar needs. However, because we do have some different needs,
there will be things on the PCB that our team will not use.

For a more in-depth look at the PCB, click [here](pages/pcb.md).

## GPS
Here's what our GPS looks like:

[]

It's function should be pretty self-explanatory. 

## Front Motor

This is our front motor. Beneath our front motor is our Encoder, shown here:

### A brief interlude about Encoders

An encoder translates information from one format to another. Our team uses it to **. 

## Rear Motor

This is our rear motor. You will notice that this is an image of the rear wheel. This is not a mistake. :)

## Landing Gear
[insert image of landing gear here]

This is our landing gear, named after how planes have landing gear wheels (fun
fact: CUAir does not use landing gear for their planes, as they prefer to just
crash land their plane each time, so we're the only project team that uses
landing gear). They're essentially a pair of fancier training wheels in that
they can lift up and down.

Their purpose is to be able to stabilize the bike while the bike is not in
immediate motion, and to try to prevent fewer falls for the bike, which can damage the parts of the bike and be quite costly. 
