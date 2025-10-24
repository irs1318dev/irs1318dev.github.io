# Encoders

Encoders are used to measure how much an axle has rotated. There are different types of encoders (optical, magnetic). We typically use a quadrature encoder, which can detect both the amount and direction of rotation.

Each encoder has a rating for how many “pulses” or ticks it produces in a complete rotation of the axle. Using simple math based on wheel (and gear) sizes, you can calculate how far something has traveled.

In WPILib, you typically use an Encoder object, which can return the number of ticks/pulses, the distance (based on distance per pulse), or the velocity. In some scenarios—such as when using a TalonSRX, TalonFX, or SPARK MAX motor controller—the encoder plugs into the motor controller and is used as part of controlling the motor.

In other scenarios (for example, some absolute encoders), the sensor is actually analog. For such encoders, WPILib uses an AnalogInput, which returns a double value (rational number) between 0 V (0 degrees) and 5 V (360 degrees).
