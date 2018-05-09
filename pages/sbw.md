# Steer-By-Wire Bike 
                                                                                                 Partially written by Linda Lu                                                                                                       
                                                                                                         Steer-by-wire subteam
                                                                                                                For ENGRC 2023
                                                                                                                2018/5/9

"What an unusual name! What does it mean?" 

## Behind the Name

Our steer-by-wire bike took inspiration from the fly-by-wire control system in aircrafts which replaces mechanical flight control with an electronic control system. We have taken that idea and applied it to our steer-by-wire bike, which will incorporate both user input and an internal control system to provide a good user experience.

# Goal of the Steer-By-Wire Bike

The goal of the steer-by-wire bike is to provide comfortable balance assisted riding for a user, by taking the user input from the handlebars and consider it alongside an internal control system to give an output that provides the best user experience.

As of Spring 2018, the steer-by-wire bike functions in one-to-one mode, i.e. the wheel always tries to follow the handelbar. However, we are working towards providing balance asistance while still mimicking the feeling of a real bike. Right now our steer-by-wire subteam is working on tuning the balance controller and PID controller on the bike, so we can prevent user from making turns that will throw a real bike off balance. The details of the controllers will be explained in later section.

# Breakdown of the Bike

So, how is the steer-by-wire bike different from the Bike?

For the most part, the steer-by-wire bike is similar to our current bike. They use the same kind of electronics, IMU, etc. The main difference is that our steer-by-wire bike has two encoders instead of one, one to take in the wheel input and one to take in the handlebar input, while the Bike only has one encoder to take in the wheel input. This is because the user input for the Bike is from the navigation algorithm, which gives a digital input. However, on our steer-by-wire bike, the input is not from a navigation algorithm but from the user handlebar input, so we need an encoder to tell us the location of the handlebar so we can translate the position to a digital signal. For those unfamiliar with encoders, they translate motion (i.e. speed and position) into an electrical signal. The use of the two encoders means that the steer-by-wire bike has no physical connection between the handlebar and the wheel, making it possible for us to add additional internal control to guide the bike than just taking input from the handlebar. 

The steer-by-wire bike also has different physical parameters such as the location of the center of mass (COM) that will make it react differently to disturbances compared to the Bike. 


# Current work

Presently, we are working on tuning the balance controller and PID controller on the steer-by-wire bike. 

To make the bike balance well and provide smooth user experience, a robust PID controller is a must. A good PID controller can ensure that our directions are executed by the wheel in an accurate and responsive way. The PID controller is essentially three constant terms that we use to determine our motor output, proportional term (P), Integral term (I) and Derivative term (D). Therefore, a PID controller continuously commands an output proportional to a measured error, its integral and its derivative. On our bike, we only consider the proportional and derivative terms; we apply a correction that is linear in displacement and velocity: output=k1x+ k2v.

We need a PID controller, defined by the pair of constants k1 and k2, that can go to the desired position the fastest with overshoot below a threshold given a possible displacement in real-life situation. However, these two constants are not linearly separable in the solution to the equation of motion which determines the optimal output that achieves our goal, so we cannot just tune them independently. Furthermore, the motor is difficult to characterize, so we are determining the optimal gains experimentally by analyzing the responses of different set of gains. 

We plan to first start tuning the controller by eye to improve the gains. Firstly, we will turn up the proportional gains to decrease lagging as the current proportional gain on the bike is visibly slow; we would continue to do so until the overshoot starts to be significant (i.e. turning the handlebar slightly causes the wheel to become jittery), indicating that we must now increase the derivative gains to prevent too much overshoot, so that the wheel is not only sensitive to position but it will also be sensitive to velocity and limit the response when velocity is high. Note that the balance controller must be off during PID controller testing to ensure that it is tested in isolation.

Once we have a good PID controller, we can start tuning the balance controller. and better evaluate . Since the motor directly takes input from the PID controller and the PID controller takes input from the balance controller, we can't correctly evaluate how the balance controller is working without a good PID controller. Like the balance controller on the Bike, the balance controller on the steer-by-wire bike is derived from the equation of motion (EOM) of a point mass model of the bike; with some reasonable assumptions (detailed in Fall 2017 final report), it can be rewritten as an equation with four variables: lean angle, lean angle rate, steer angle and steer angle rate. Therefore, we can represent the steer angle rate as a linear combination of the other three variables and generate a steer angle rate output to the motor to maintain equalibrium based on the known values of the other three variables. Just like the PID controller, the balance controller is essentially a set of three constant terms (i.e. gains) that will be multiplied by the three variables to obtain an optimal steer angle rate that maintains equalibrium. So we need to find a good set of gains that can prevent the bike from falling in various situations.

As of now, we are trying to find the best set of gains using grid search, which simulates the linearized bike model in MATLAB for every possible set of gains in a given search space and observes their performance. To quantitatively compare their performance, we use a scoring system to rank them. The scoring criteria is somewhat arbitrary; a big part of improving the balance controller gains is improving the scoring criteria to mimic a real world situation so that a set of gains that is successful in simulation can be successful during testing. 

In the future, we also plan on implementing gains scheduling to find optimal gains separately for various speeds for more precise optimization. Our current simulation are based on a velocity of 3 m/s; however, the dynamics will change with respect to the speed, so switching out gains based on the speed is a sensible approach.
