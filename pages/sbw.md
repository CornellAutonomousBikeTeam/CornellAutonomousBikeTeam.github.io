# Steer-By-Wire Bike 
                                                                                                    By Linda Lu
                                                                                                    Steer-by-wire subteam
                                                                                                    For ENGRC 2023

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

For the most part, the steer-by-wire bike is similar to our current bike. They use the same kind of electronics, IMU, etc. The main difference is that our steer-by-wire bike has two encoders instead of one, one to take in the wheel input and one to take in the handlebar input, while the Bike only has one encoder to take in the wheel input. This is because the user input for the Bike is from the navigation algorithm, which gives a digital input. However, on our steer-by-wire bike, the input is not from a navigation algorithm but from the user handlebar input, so we need an encoder to tell us the location of the handlebar so we can translate the position to a digital signal. For those unfamiliar with encoders, they translate motion (i.e. speed and position) into an electrical signal. The use of the two encoders means that the steer-by-wire bike has no physical connection between the handlebar and the wheel, making it possible for us to add additional internal control to guide the bike than just taking input from the handlebar. 

The steer-by-wire bike also has different physical parameters such as the location of the center of mass (COM) that will make it react differently to disturbances compared to the Bike. 



# Current work

Presently, we are working on tuning the balance controller and PID controller on the steer-by-wire bike. 

To make the bike balance well and provide smooth user experience, a robust PID controller is a must. A good PID controller can ensure that our directions are executed by the wheel in an accurate and responsive way. The PID controller is essentially three constant terms that we use to determine our motor output, proportional term (P), Integral term (I) and Derivative term (D). Therefore, a PID controller continuously commands an output proportional to a measured error, its integral and its derivative. On our bike, we only consider the proportional and derivative terms; we apply a correction that is linear in displacement and velocity: output=k1x+ k2v.

We need a PID controller, defined by the pair of constants k1 and k2, that can go to the desired position the fastest with overshoot below a threshold given a possible displacement in real-life situation. However, these two constants are not linearly separable in the solution to the equation of motion which determines the optimal output that achieves our goal, so we cannot just tune them independently. Furthermore, the motor is difficult to characterize, so we are determining the optimal gains experimentally by analyzing the responses of different set of gains. 

We plan to first start tuning the controller by eye. Firstly, we will turn up the proportional gains to decrease lagging as the current proportional gain on the bike is visibly slow; we would continue to do so until the overshoot starts to be significant (i.e. turning the handlebar slightly causes the wheel to become jittery), indicating that we must now increase the derivative gains to prevent too much overshoot, so that the wheel is not only sensitive to position but it will also be sensitive to velocity and limit the response when velocity is high. After we have 

