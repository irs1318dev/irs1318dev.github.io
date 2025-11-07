# PID Controllers

"PID" stands for **P**roportional, **I**ntegral, and **D**erivative. PID is a way of controlling a part of a robot that incorporates feedback from sensors to control the operation of the robot. PID is often used to correct for error caused by things like friction or other forces pushing back on the robot. PID takes in the current measured value (the value from an encoder or other sensor) and a setpoint (the desired value).

We typically use PID for elevators and for positional control in the drivetrain. For velocity control, we also use feedforward to provide additional control ("PIDF" controller).

## How does PID work?
PID works through a "simple" calculation comparing the difference between the setpoint and the measured value, called error.

$error = setpoint - measuredValue$

The control signal applied to the motor is calculated based on the error, and how the error changes or accumulates over time.  Essentially, the control signal is based on the sum of a few components: the proportional constant multiplied by the error, the derivative constant multiplied by the rate-of-change of the error, and the integral constant multiplied by the weighted sum of the error over time.

$controlSignal = k_P * error + k_I * \int error * dt + k_D * \frac{derror}{dt}$

For some scenarios, we add in an additional term for "feed-forward" control in addition to the "feed-back" control.  The feed-forward term ($k_F$) is typically a constant simply multiplied by the setpoint.  When feed-forward is used, it is called a "PIDF" controller.

$controlSignal = k_P * error + k_I * \int error * dt + k_D * \frac{derror}{dt} + k_F * setpoint$

## How can we think of the constants/gains used for PID?
With PID, the constant values typically need to be discovered experimentally for the P, I, D, and F gains. Typically, F is only used for velocity control. P is used for essentially all PID controllers. I is used to correct error from slight overshoots or undershoots over time. D is used to reduce oscillation around the setpoint.

## Tuning PID
Typically, we follow a system like the below to tune PID:

1. Determine the typical behavior/ranges of the system (system identification) using direct control (e.g. Percent output). For Positional PID systems, see if there is a certain range of measured values that can be read from the sensor around the expected range for the system. For all systems, but especially Velocity PID systems, try to check the min and max power levels to see the min and max velocities (measured values over time) that can be seen by the sensor.

2. Start tuning the proportional gain. Start with a small value for the $k_P$ constant. The specific value ranges depend on the system - different controllers expect different ranges for the Control Signal, and different systems measure values from the sensors in different ways. Enable the system with a setpoint of wherever it currently is, and then change the setpoint to another value. You can then judge how good of a proportional gain was chosen based on the behavior. When it is too low, the system never reaches the setpoint - double the gain and try again. When it is too high, the system oscilates around the setpoint - start splitting the difference between the value that was too low and the one that was too high.

3. If there is still oscilation around the setpoint, add derivative gain ("dampening"). Start with a small value for the $k_D$ constant. It can be harder to tune this because too high looks very similar to too low. So there may need to be some luck to finding a value that is helpful and not harmful.

4. If the system needs an extra push to reach the setpoint, add integral gain. Start with a small value for the $k_I$ constant.

For more information, Wikipedia has an okay article on PID.
