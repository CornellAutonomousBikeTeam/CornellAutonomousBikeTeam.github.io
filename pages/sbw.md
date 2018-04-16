# Steer-By-Wire Bike

"What an unusual name! What does it mean?" 

## Behind the Name

Prior to the 1960s, planes were steered directly. Any turn that the pilot applied to the pilot controls would result in a
direct change to the flight controls. 

In the 1960s, planes began to develop a fly-by-wire system. In this system, when a pilot applies a turn to the pilot controls,
electronic commands were sent to the system that would then determine, based off a combination of internal and external factors, how much the flight controls would be moved. 

We have taken that idea and applied it to our steer-by-wire bike, which will incorporate both user input and an internal control system to provide a good user experience.

# Goal of the Steer-By-Wire Bike

The goal of the steer-by-wire bike is to provide comfortable assisted riding for a user, by taking the user input from the handlebars and consider it alongside an internal control system to give an output that provides the best user experience.
Presently, the steer-by-wire bike works in one-to-one mode, i.e. the handlebar input is directly translated into a motor output. However, we are working towards providing riding asistance by helping user balance while still mimicking the feeling of a real bike.
To this end, our steer-by-wire subteam is working on tuning the balance controller and PID controllers on the bike, so we can prevent user from making rapid or extreme turns that will throw a real bike off balance. The details of the controllers will be explained in later section.

# Breakdown of the Bike

So, how is the steer-by-wire bike different from the Bike?
For the most part, the steer-by-wire bike is similar to our current bike. They use the same kind of electronics, IMU, etc. The main difference is that our steer-by-wire bike has two encoders instead of one, one to take in the wheel input and one to take in the handlebar input, while the Bike only has one encoder to take in the wheel input. This is because the user input for the Bike is from the navigation algorithm, which gives a digital input. However, on our steer-by-wire bike, the input is not from a navigation algorithm but from the user handlebar input, so we need an encoder to tell us the location of the handlebar so we can translate the position to a digital signal. For those unfamiliar with encoders, they translate motion into an electrical signal.
Besides the use of the two encoders, the steer-by-wire bike also has different physical parameters
# Current work
