# Distance Sensors

There are various types of distance sensors, which use either sound or light to sense how far the robot is from an object. In WPILib, you would use an AnalogInput, which returns a double value (rational number) indicating how many volts were detected by the sensor.

This value will differ based on the sensor and its placement, so experimentation is needed to interpret the readings. It is also possible to use a more complex sensor that requires custom code to communicate via I2C or another protocol with the RoboRIO.
