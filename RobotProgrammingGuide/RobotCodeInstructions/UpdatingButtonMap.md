# Updating ButtonMap

After adding a new operation, open the `ButtonMap.java` file (under `core_robot\\src\\main\\java\\frc\\robot\\driver`) and add a mapping into the schema that corresponds to the type of operation being added (analog, digital, macro). Remember that analog operations represent things that are done to a certain extent, using double (decimal) values typically between -1.0 and 1.0. Digital operations represent things that are either done or not done, using boolean values (true or false). Each type of operation, analog or digital, has its own corresponding type of `OperationDescription`.

## Adding Analog Operation Descriptions

```java
    new AnalogOperationDescription(
        AnalogOperation.DriveTrainTurn,
        UserInputDevice.Driver,
        AnalogAxis.XBONE_RSX,
        ElectronicsConstants.INVERT_XBONE_RIGHT_X_AXIS,
        TuningConstants.DRIVETRAIN_X_DEAD_ZONE),
```

The analog description takes parameters describing the user input device (driver or co-driver controller) and the axis of the joystick (X, Y, throttle, etc.). Different controller types support different axes and use different enumeration values, so make sure to select one that makes sense and is consistent for your controller type. The description also includes the ability to invert the axis (so that pressing the joystick in a certain direction matches its positive/negative value) and to provide a dead zone (as joysticks are often imperfect at measuring the middle, so it can be useful to ignore a certain range around the center).

## Adding Digital Operation Descriptions

```java
    new DigitalOperationDescription(
        DigitalOperation.IntakeIn,
        UserInputDevice.Codriver,
        UserInputDeviceButton.XBONE_A_BUTTON,
        ButtonType.Simple),
```

The digital description takes arguments describing the user input device, the button on the controller (or certain alternatives), and the type of button (Simple, Toggle, or Click). Simple buttons are typically used for continuous actions (such as running an intake). Toggle actions are typically used for macros. Click actions are typically used for single-shot actions (such as extending an arm) or changing state (enable mode or disable mode). Some alternatives to using a button on the controller include a POV direction or an `AnalogAxis` with a range of triggering values.

## Adding Shifts

```java
    new ShiftDescription(
        Shift.DriverDebug,
        UserInputDevice.Driver,
        UserInputDeviceButton.XBONE_SELECT_BUTTON),
```

A shift description takes arguments describing the user input device and the button on the joystick (or certain alternatives). Whenever that button is pressed, the shift is active, and it is inactive when released. Some alternatives to using a button on the controller include a POV direction or an `AnalogAxis` with a range of triggering values.

## Using OperationContext and Shifts

In addition to `UserInputDevice` and `UserInputDeviceButton`/`UserInputDevicePOV`/`AnalogAxis`, you can add modifiers that control when to register certain button presses. One is called `OperationContext`, where the operation is only considered when the robot is in a certain mode based on the current state of the mechanisms. Another is called `Shift`, where the operation is only considered when a certain combination of other buttons are pressed (or not pressed) according to the configuration. For each of these, they’re specified using an `EnumSet`.

To enable an operation during all operation contexts (the default), specify `EnumSet.allOf(OperationContext.class)`. To enable an operation only during an operation context called "Extended," specify `EnumSet.of(OperationContext.Extended)`.

To enable an operation when the shift button `DriverDebug` is pressed, specify relevant shifts of `EnumSet.of(Shift.DriverDebug)` and required shifts of `EnumSet.of(Shift.DriverDebug)`. To enable an operation when the shift button `DriverDebug` is not pressed, specify relevant shifts of `EnumSet.noneOf(Shift.class)`.
