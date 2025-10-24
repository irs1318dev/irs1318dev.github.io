# Writing a New Mechanism

Mechanisms handle the interactions with the actuators (e.g., motors, pneumatic solenoids) and sensors (e.g., encoders, limit switches) of each part of the robot, controlling them based on operations from the driver. A mechanism is a class that implements the `IMechanism` interface, with a name based on that portion of the robot (e.g., `DriveTrain`, `Intake`) combined with "Mechanism," such as `IntakeMechanism`. Place it within the `mechanisms` folder (under `core_robot/src/main/java/frc/robot/mechanisms`) with the other mechanisms and managers.

## Define mechanism class and member variables

```java
package frc.robot.mechanisms;

@Singleton
public class ThingMechanism implements IMechanism
{
  // driver
  private final IDriver driver;

  // sensors and actuators
  private final ISomeSensor nameOfSensor;
  private final ISomeActuator nameOfActuator;

  // logger
  private final ILogger logger;

  // sensor values
  private boolean someSetting;

  // mechanism state
  private boolean someState;
```

At the top of the file, indicate the package (which should be `frc.robot.mechanisms`) and then define the class with the `@Singleton` annotation. Within the class, first define the driver (`private final IDriver driver;`), and then define each of the actuators and sensors controlled by the mechanism (`private final ISomeActuator nameOfActuator;` and `private final ISomeSensor nameOfSensor;`, using the proper type for the sensors/actuators). These will all be initialized in the constructor. After the driver and the set of actuators and sensors are defined, you may also need to define the logger (`private ILogger logger;`), anything that will be read from the sensors (`private boolean someSetting;`), and any state that needs to be kept for the operation of the mechanism (`private boolean someState;`). The types of the values read from sensors depend on the types of sensor involved, and the types of any state depend on the way the mechanism is expected to work.

## Write mechanism constructor

```java
  @Inject
  public ThingMechanism(IDriver driver, IRobotProvider provider, LoggingManager logger)
  {
    this.driver = driver;

    this.nameOfSensor = provider.getSomeSensor(ElectronicsConstants.THING_NAMEOFSENSOR_DIO_CHANNEL);
    this.nameOfActuator = provider.getSomeActuator(ElectronicsConstants.THING_NAMEOFACTUATOR_PWM_CHANNEL);

    this.logger = logger;

    this.someSetting = false;
    this.someState = false;
  }
  ...
```

After defining all of the class's variables, define a constructor like `public ThingMechanism(IDriver driver, IRobotProvider provider, LoggingManager logger)`. Since 2017 we’ve used Google Guice to handle dependency injection, which is why the `@Inject` annotation is required. Guice can provide some of the parameters that you need, including the `IDriver`, `IRobotProvider`, and `LoggingManager`. It can also provide an `ITimer` if needed. Within the constructor, first set the class's driver member to the value that is passed in. Then set the value for each actuator and sensor you defined earlier by calling the corresponding function on the `IRobotProvider` that is also passed into the constructor. These functions will take arguments based on how the actuators/sensors are physically plugged together in the robot (such as CAN IDs, DIO channel, analog channel, PCM channel, or PWM channel). These arguments should be placed as constants in the `ElectronicsConstants` file with names such as `THING_NAMEOFACTUATOR_PWM_CHANNEL`. We don’t necessarily know in advance how the robot plugs together, so they can be initialized with a value of -1 until we do. After initializing the sensors and actuators, set the logger as provided and initialize settings and state to their default values.

## Write mechanism readSensors function

```java
  @Override
  public void readSensors()
  {
    this.someSetting = this.nameOfSensor.get();

    this.logger.logBoolean(LoggingKey.ThingSomeSetting, this.someSetting);
  }
```

The `readSensors()` function reads from the relevant sensors for that mechanism, stores the results in class member variables, and then logs the results. Most simple sensor types have a `get()` function (or similar) to read the current value. Sometimes there are functions named something like `getXX()` to get more specific data about "XX." An entry in the `LoggingKey` enum will need to be added to correspond to each thing that we want to log.

## Write mechanism update function

```java
  @Override
  public void update(RobotMode mode)
  {
    boolean shouldThingAction = this.driver.getDigital(DigitalOperation.ThingAction);

    double thingActionAmount = 0.0;
    if (shouldThingAction)
    {
      thingActionAmount = TuningConstants.THING_ACTION_AMOUNT;
    }

    this.nameOfActuator.set(thingActionAmount);
    this.logger.logNumber(LoggingKey.ThingActionAmount, thingActionAmount);
  }
```

The `update()` function examines the inputs that we retrieve from the `IDriver`, calculates the outputs, and applies them to the relevant actuators. For some mechanisms, the logic will be very simple—reading an operation and applying it to an actuator. Other mechanisms will involve some internal state and information from the most recent sensor readings, and possibly some math to determine what the actuator should do. Note that there will often be a degree to which something should be done that we don't know in advance. For example, if we are intaking a ball we may want to carefully choose the correct strength to run the motor. Because we don't know this value in advance and will discover it experimentally, we should put such values into the `TuningConstants` file as constants with a starting guess. Finally, we can add another `LoggingKey` enum entry and log the value that we decided to use for the actuator.

## Write mechanism stop function

```java
  @Override
  public void stop()
  {
    this.nameOfActuator.set(0.0);
  }
```

The stop function tells each of the actuators to stop moving. This typically means setting any motor to 0.0 and any `DoubleSolenoid` to `Off`, or calling the `stop()` function on the actuator if one is present. It is called when the robot is being disabled, and it is very important to stop everything to ensure that the robot is safe and doesn't make any uncontrolled movements.

## Write any getter functions

```java
  public boolean getSomeSetting()
  {
    return this.someSetting;
  }
```

When sensors are being read, we often want to incorporate that data into the running of tasks as part of macros and autonomous routines. To support that, add getter functions so tasks can access the values that were read from the sensors. These functions simply return the value that was read during the `readSensors()` function. Typically, we can skip writing these until a task being written needs this information.
