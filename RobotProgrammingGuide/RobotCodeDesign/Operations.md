# Operations

An operation is a single basic action that the robot can perform. There are typically many operations for each mechanism. These operations should be thought of as the most basic ways of controlling each mechanism. Operations are also the building blocks on top of which we build macros and autonomous routines. Operations can be either analog or digital.

## Analog Operations

Analog operations typically happen to a certain extent and are controlled by an axis on the joystick during teleop mode (e.g., the drivetrain is controlled by pushing forward along the Y axis of the joystick). Analog operations are represented by double values (rational number, usually between -1.0 and 1.0). Analog operations are defined in the `AnalogOperation` enumeration.

## Digital Operations

Digital operations either happen or do not happen and are controlled by a button on the joystick or button pad during teleop mode (e.g., a trigger on the joystick to cause a "shoot" action). Digital operations are represented by boolean values (true or false). Digital operations are defined in the `DigitalOperation` enumeration.

There are three main types of digital operations:

-   Simple: "true" (on) whenever the button is actively being pressed, and "false" (off) otherwise. A simple button would typically be used for spinning an intake roller while trying to pick up a ball. A real-world example of a simple button would be something like the Shift key on a computer keyboard.
-   Toggle: "true" from the time it is first pressed until the next time it is pressed, and then false until it is pressed again. A toggle button is typically used for running a macro. A real-world example of a toggle button would be the Caps Lock key on a computer keyboard.
-   Click: true the first time we run an update after each button press, and false until the button has been released and pressed again. A click button would typically be used for shooting a ball or lifting an arm. A real-world example would be a momentary push-button.

**Note**: Although it often feels like toggle buttons make sense for enabling/disabling certain modes, they can be confusing for a driver who may not be able to tell the current mode. Much like someone typing with Caps Lock if they aren’t paying attention to the screen, a driver could inadvertently not notice whether they are currently in the expected mode if there isn’t a good indicator on the robot. For this reason, we typically use two separate `EnableX` and `DisableX` click operations instead of toggles.
