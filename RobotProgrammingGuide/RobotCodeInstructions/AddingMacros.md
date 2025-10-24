# Adding Macros

Macros provide a way to automatically execute one or more actions in a predictable fashion to make the robot’s operation more precise or to provide convenient controls for the human driver or co-driver. Macros use a series of control tasks working together to accomplish these actions.

To add a new macro, add a new entry to the `MacroOperation` enumeration and a new `MacroOperationDescription` to the macro schema within the `ButtonMap` class.

```java
new MacroOperationDescription(
    MacroOperation.SomeMacro,
    UserInputDevice.Driver,
    UserInputDeviceButton.XBONE_X_BUTTON,
    ButtonType.Toggle,
    () -> new SomeTask()),
```

The `MacroOperationDescription` requires arguments describing the user input device to use, the button that triggers the macro, the type of button to use (either `Simple` or `Toggle`), and a supplier for the task that should be used within the macro (`() -> new SomeTask()`).
