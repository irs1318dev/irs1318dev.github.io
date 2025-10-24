# Adding a New Tuning Constant

To add a new constant that holds a "magic value" that can be updated to adjust how the robot behaves, first open the `TuningConstants` class (TuningConstants.java under `core_robot\src\main\java\frc\robot`) and add a new constant value. We try to keep the various constants organized, so we list them in a different section for each mechanism. Each constant is of the form:

```java
    public static final Type NAME_YELLING_SNAKE_CASE = value;
```

The type depends on what is being tracked, usually an `int`, `double`, or `boolean`.

The naming convention for our tuning constants is `MECHANISMNAME_COMPONENTNAME_DESCRIPTION`. The name uses "yelling snake case," which is an all-caps form of snake case where each word or compound word is separated by the underscore character `_`. Within the name, `MECHANISMNAME` is a form of the mechanism’s name (e.g., `ELEVATOR` or `DRIVETRAIN`). `COMPONENTNAME` is a form of the component’s name (e.g., `ENCODER`, `LEFT_MOTOR`, or `ARM`). And `DESCRIPTION` is a description of what is being tuned, such as the number of ticks per rotation in an encoder, a gear ratio, or the length of an arm segment.
