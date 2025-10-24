# Adding Operations

To add a new action that the robot can take with a mechanism, first open the `AnalogOperation` or `DigitalOperation` enum (AnalogOperation.java or DigitalOperation.java under `core_robot\src\main\java\frc\robot\driver`) and add a new value to the list in that file. We try to keep the various operations organized, so we list them in a different section for each mechanism.

Digital operations are all-or-nothing, expressed as a true or false value (type `boolean`).

Analog operations are done to some extent, expressed as a decimal number (type `double`, a double-precision floating-point number).

The operation should be named starting with the mechanism (e.g., "DriveTrain", "Intake", etc.), followed by a description of the action (e.g., "Turn", "RaiseArm", etc.) to make a single PascalCase value (e.g., "DriveTrainTurn", "IntakeRaiseArm").

Remember that analog/digital operations represent single, simple actions performed by the robot. Any more complex action we want the robot to take will be a macro that composes these operations together.
