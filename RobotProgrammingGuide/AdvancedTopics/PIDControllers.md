# PID Controllers

"PID" stands for **P**roportional, **I**ntegral, and **D**erivative. PID is a way of controlling a part of a robot that incorporates feedback from sensors to control the operation of the robot. PID is often used to correct for error caused by things like friction or other forces pushing back on the robot. PID takes in the current measured value (the value from an encoder or other sensor) and a setpoint (the desired value).

We typically use PID for elevators and for positional control in the drivetrain. For velocity control, we also use feedforward to provide additional control.

With PID, there are constant values that need to be discovered experimentally for the P, I, D, and F gains. Typically, F is only used for velocity control. P is used for essentially all PID controllers. I is used to correct error from slight overshoots or undershoots over time. D is used to reduce oscillation around the setpoint. For more information, Wikipedia has an okay article on PID.
