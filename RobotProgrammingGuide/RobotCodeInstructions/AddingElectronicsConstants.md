# Adding a New Electronics Constant

To add a new constant that describes how the robot is wired/configured electronically, first open the `ElectronicsConstants` class (ElectronicsConstants.java under `core_robot\src\main\java\frc\robot`) and add a new constant value. We try to keep the various constants organized, so we list them in a different section for each mechanism. Each constant is of the form:

```java
    public static final Type NAME_YELLING_SNAKE_CASE = value;
```

The type is almost always an integer `int` for electronics constants, representing the port where something is plugged in or an ID that has been assigned to the component. The type may depend on the interface being used.

The naming convention for our electronics constants is `MECHANISMNAME_COMPONENTNAME_INTERFACE`. The name uses "yelling snake case," which is an all-caps form of snake case where each word or compound word is separated by the underscore character `_`. Within the name, `MECHANISMNAME` is a form of the mechanism’s name (e.g., `ELEVATOR` or `DRIVETRAIN`). `COMPONENTNAME` is a form of the component’s name (e.g., `ENCODER` or `LEFT_MOTOR`). `INTERFACE` is one of a few possible values that describe which interface the component is connected through. Most components are connected using a single interface, such as sensors connected to a `DIO_CHANNEL` for digital inputs or an `ANALOG_CHANNEL` for analog inputs; motors connected to a `PWM_CHANNEL`; or motors using a specific `CAN_ID` when connected through the CAN bus. Some components use two interfaces, such as `FORWARD_PCM_CHANNEL` and `REVERSE_PCM_CHANNEL` for double solenoids (pneumatics) and `DIO_CHANNEL_A` and `DIO_CHANNEL_B` for simple quadrature encoders.

Lastly, the value is the specific port the component was plugged into or the ID that was assigned to the component.
