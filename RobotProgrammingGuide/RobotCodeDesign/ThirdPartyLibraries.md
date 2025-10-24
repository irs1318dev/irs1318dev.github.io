# External Libraries

The robot code makes use of a number of external libraries in order to make programming the robot more straightforward.

## Guice

[Guice](https://github.com/google/guice) (pronounced "juice") is a dependency injection library responsible for the various `@Inject` and `@Singleton` annotations seen throughout the code. The purpose of Guice is to make it easier to plug together the entire system so it is unit-testable and able to be simulated in Fauxbot. You will need to use Guice’s `@Singleton` and `@Inject` annotations when writing a mechanism.

## CTRE Phoenix

[CTRE Phoenix](https://docs.ctr-electronics.com/) is a library that provides the ability to communicate with and control various motors using the Talon SRX, Talon FX, and Victor SPX over CAN. We use CTRE Phoenix to control the majority of our Talon SRX/Talon FX controllers so that we can run PID on the controller itself for a faster update rate.

## Spark MAX API

The [SPARK MAX](http://www.revrobotics.com/sparkmax-software/) has a library that provides the ability to communicate with and control motors using the SPARK MAX over CAN. We use the SPARK MAX to control NEO motors so that we can use these brushless motors and run PID on the SPARK MAX itself for a fast update rate.

## JUnit

[JUnit](https://junit.org/junit4/) is a unit testing library for Java. JUnit is fairly simple and provides comparison functions and a framework for running unit tests.

## Mockito

[Mockito](http://site.mockito.org/) is a library for mocking objects for unit testing. Mockito provides a way to create fake versions of objects with behaviors you can describe succinctly.

## OpenCV

[OpenCV](https://opencv.org/) is a computer vision library used for fast and efficient image processing. We use OpenCV functions to capture images, manipulate them (undistort, HSV filtering), write them, and discover important parts of them (find contours).

## AprilTag

[AprilTag](https://github.com/AprilRobotics/apriltag) is a computer vision library used for finding and using AprilTag fiducials in images. Most of the code directly interacting with the AprilTag library is already written and won’t need significant regular updates.
