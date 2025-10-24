# Pneumatics

Pneumatic cylinders are also used to provide movement for components on the robot. They provide linear force and are controlled by a pair of valves (solenoids) that route air pressure to move the rod within the cylinder.

There are three settings:

-   Off: No air pressure is applied through either valve.
-   Forward: Air pressure is applied through one valve.
-   Reverse: Air pressure is applied through the other valve.

Forward and reverse typically correlate to whether the piston is actively pushing out or pulling in, but this depends on how the pneumatics are set up.

Because of how they work, solenoid-controlled pneumatics trigger all-or-nothing movements. Pneumatics are often used in shooters (such as the kicker on the 2016 robot) or for controlling the position of an intake (such as on the 2019 robot). In WPILib, they are controlled using Value.kOff, Value.kForward, and Value.kReverse.
