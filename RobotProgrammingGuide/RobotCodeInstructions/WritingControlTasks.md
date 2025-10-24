# Writing Control Tasks

Tasks control operations or groups of operations that run until a certain condition is met. A task is a class that implements the `IControlTask` interface and typically extends `ControlTaskBase`, `TimedTask`, `CompositeOperationTask`, or `ConditionalTask`. Tasks are named based on the action they perform (e.g., `RaiseElevator`) combined with "Task," such as `RaiseElevatorTask`. Place the class within the `controltasks` folder (under `core_robot/src/main/java/frc/robot/driver/controltasks`) with the other tasks.

## Define task class, member variables, and constructor

```java
public class RaiseElevatorTask extends ControlTaskBase implements IControlTask
{
  private ElevatorMechanism elevator;

  public RaiseElevatorTask()
  {
  }
}
```

At the top of the class, declare any member variables that you need. Some of these may be initialized in the constructor (for example, when your task has parameters like a time duration), whereas others will be initialized in the `begin()` function. Note that the constructor could be called well before the task actually starts, which is why we have the `begin()` function below.

## Write task begin function

```java
public void begin()
{
  this.elevator = this.getInjector().getInstance(ElevatorMechanism.class);
}
```

The `begin()` function is called at the very beginning of the task and can be used to set initial state and retrieve any mechanism that we need to reference. Note that this function is called right before `hasCompleted()` and `update()` are called for the first time.

## Write task update function

```java
public void update()
{
  this.setDigitalOperationState(DigitalOperation.ElevatorRaise, true);
}
```

The `update()` function is called every ~20 ms and should update the relevant operations.

## Write task end function

```java
public void end()
{
  this.setDigitalOperationState(DigitalOperation.ElevatorRaise, false);
}
```

The `end()` function is called when the task has ended. The function resets the operations that were used to their default values and should clear any state that needs to be cleared.

## Write task hasCompleted function

```java
public boolean hasCompleted()
{
  return this.elevator.isRaised();
}
```

The `hasCompleted()` function is called by the `Driver` class to check whether the particular task should complete. Often this is based on either the amount of time that has elapsed since the task began, or it could be based on some sensor condition being met.

## Write task shouldCancel function (optional)

```java
public boolean shouldCancel()
{
  return this.elevator.isBroken();
}
```

The `shouldCancel()` function is called by the `Driver` class to check whether the task should be cancelled prematurely. This is used in a few situations, such as when we are unable to perform an action anymore because a precondition is not met.

## Write task stop function (optional)

```java
public void stop()
{
  this.setDigitalOperationState(DigitalOperation.ElevatorRaise, false);
}
```

The `stop()` function is called when the task has been cancelled or interrupted. The function resets the operations that were used to their default values and should clear any state that needs to be cleared. Typically, tasks do the same thing during `stop()` as they do during `end()`, so when that is the case only `end()` needs to be implemented/overridden.
