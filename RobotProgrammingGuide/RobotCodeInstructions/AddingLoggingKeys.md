# Adding a New Logging Key

To add a new key for logging purposes, first open the `LoggingKey` enum (LoggingKey.java) and add a new value to the list in that file. We try to keep the various logging keys organized by mechanism, so please keep them sorted in a sensible order. Each logging key is of the form below, with a given name, and with the first parameter being the name displayed in the dashboard, the second being the type, and the third being whether it is an input from a sensor (true) or not (false):

```java
    Name("value", LoggingType.String, false),
```

The name is of the form `MechanismComponentState`, where the first part is the name of the mechanism (e.g., `Intake` or `DriveTrain`), the second part (if relevant) is the component within that mechanism that is affected (e.g., `Arm`), and the last part is the state being logged (e.g., `IsExtended` or `LeftDistance`). The name uses PascalCase, where multiple words are included and separated by capitalizing the first letter of each word.

The value is of the form `m/state`, where the first part is an abbreviation for the mechanism (e.g., `i` for intake or `dt` for drivetrain) that is unique for the mechanisms on the robot, and the second part is a camelCase form of the state. In addition to the value, the enum also needs to describe the type of value being logged and whether it is considered an input to the system or an output/calculated value. The `LoggingType` could be a boolean, decimal number, integer, string, nullable number, or nullable integer.

Put together, an entry for a differential (tank) drivetrain’s left distance would look like:

```java
    DriveTrainLeftDistance("dt/leftDistance", LoggingType.Number, true),
```
