# Composing Tasks Together

Tasks can be grouped in interesting ways to describe more complex behavior. By having tasks happen in a certain order and sometimes simultaneously, you can build a complex task out of simpler, reusable tasks. To do this, you can use `SequentialTask`, `ConcurrentTask`, and `ConditionalTask`-based tasks.

## SequentialTask.Sequence()

`SequentialTask` starts and completes each task in the order they are listed.

```java
SequentialTask.Sequence(
  new WaitTask(3.0),
  new DriveForwardTask(3.5));
```

The example above is a sequence of two tasks: first wait 3 seconds, then drive 3.5 inches forward.

## ConcurrentTask.AnyTasks()

`ConcurrentTask.AnyTasks` starts all tasks at the same time and completes when any one of them has completed.

```java
ConcurrentTask.AnyTasks(
  new WaitTask(3.0),
  new DriveForwardTask(3.5));
```

The example above runs two tasks at the same time, completing when either 3 seconds have elapsed OR the robot has driven 3.5 inches forward.

## ConcurrentTask.AllTasks()

`ConcurrentTask.AllTasks` starts all tasks at the same time and completes when all of them have completed.

```java
ConcurrentTask.AllTasks(
  new WaitTask(3.0),
  new DriveForwardTask(3.5));
```

The example above runs two tasks at the same time, completing when 3 seconds have elapsed AND the robot has driven 3.5 inches forward.

## ConditionalTask-based tasks

Conditional tasks can use branching logic based on conditions within our tasks. These are implemented as classes inheriting from `ConditionalTask`, which evaluate a condition (e.g., "elevator is above level 3") and, based on that, decide which action to perform next. This allows you to create a decision tree based on different conditions so the macro or autonomous routine can respond to the current state of the robot or even the world around it.
