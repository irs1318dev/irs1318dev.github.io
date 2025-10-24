# Through-beam Sensors

Through-beam sensors are simple infrared sensors and emitters used to detect whether anything is between the light source and the receiver. They’re often used in the real world at the bottom of a garage door to detect if something is under the door so it doesn’t get crushed. On a robot, they can be used to sense whether something is in a given location. We often use them to detect whether a game piece has been successfully picked up.

In WPILib, you would use an AnalogInput, which returns a double value (rational number) indicating how many volts were detected by the infrared sensor. This value will differ based on the through-beam sensor model, so you can determine through experimentation whether it is tripped for a given value range.
