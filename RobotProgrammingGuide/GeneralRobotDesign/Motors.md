# Motors

Electric motors are typically used to provide movement for the robot. They provide rotational force that depends on their current setting and the available voltage.

Motors are useful when a specific amount of motion is needed or when motions must happen at different speeds (as opposed to all-or-nothing). They’re used in places such as drivetrains, elevators, and intakes. In WPILib, motors are controlled using a double value (rational number) between -1.0 and 1.0.

Since 2018, we have typically used the Talon SRX, which can incorporate a motor, an encoder, top/bottom limit switches, and a PID controller to allow for advanced control. In 2020, we started using brushless motors, including the Falcon with its built-in TalonFX motor controller and the NEO with its corresponding SPARK MAX motor controller.
