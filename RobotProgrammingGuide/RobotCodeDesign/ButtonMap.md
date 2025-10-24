# ButtonMap

The `ButtonMap` contains the mapping of joystick/controller buttons and axes to the corresponding digital and analog operations. The `Driver` class is in charge of reading from the joysticks and button pads during teleop mode, and it uses the `ButtonMap` schemas to translate joystick actions into `DigitalOperation`s, `AnalogOperation`s, and `MacroOperation`s.

[Shifts](Shifts.md) are also used to enhance the driver’s control options.

[Operation Contexts](OperationContexts.md)
