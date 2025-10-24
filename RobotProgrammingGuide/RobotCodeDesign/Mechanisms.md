# Mechanisms

Mechanism classes handle reading all sensors and controlling all actuators for each mechanism of the robot. There is one mechanism class for each individual part of the robot, named using the pattern `ThingMechanism` (where "Thing" is the name of the mechanism, like `DriveTrain`).

Mechanisms read from all sensors and translate the operations from the driver into the functions that need to be called on individual actuators. This typically involves math and logic to convert operation data into the actions that need to happen. For example, with a typical tank drivetrain, the `DriveTrainMechanism` calculates the speed settings to apply to the left and right motors based on the `DriveTrainMoveForward` and `DriveTrainTurn` operations. There may be additional concerns, such as responding to the presence or absence of a setting from another operation or a sensor.

Mechanisms implement the `IMechanism` interface, which defines the functions every mechanism must implement. In a mechanism, the `readSensors()` and `update()` functions are the most important and are called every ~20 milliseconds.

The `readSensors()` function reads the current values from all sensors and stores them in member variables for that mechanism object. The `update()` function calculates what should be applied to the output devices based on the current operations and the data previously read from the sensors.

It’s important that these functions execute quickly. Anything that depends on a certain amount of time elapsing should be calculated across separate runs of the function and should not involve long-running loops or sleeps. Most actions that take multiple iterations of `update()` or depend on time elapsing belong in a macro instead of being hard-coded into the mechanism, though it’s also possible to keep state in member variables to track what the mechanism should be doing.
