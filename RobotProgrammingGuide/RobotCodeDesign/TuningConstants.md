# TuningConstants

To simplify tuning the robot, we store any "magic numbers" that we’ll likely want to change as constants in the `TuningConstants` class.

Settings that may need tuning include the speed at which to run an intake or the rate at which to turn when the joystick is in a certain position. These settings are usually hard to know in advance, and the appropriate values are discovered by testing the robot. Because many details aren’t known ahead of time by the software team, organizing these values in `TuningConstants` helps speed up the tuning process and prevents bugs.
