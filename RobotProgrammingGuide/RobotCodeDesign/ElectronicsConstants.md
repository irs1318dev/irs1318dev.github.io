# ElectronicsConstants

`ElectronicsConstants` is a class that holds constant values describing all of the physical connections (PWM channels, Digital I/O channels, Analog I/O channels, CAN IDs, etc.) needed to control the correct output devices and read the correct sensors. We keep this information in a separate class (and all in a single file) so there is only one place to update if the electronics sub-team needs to re-run the wiring, or in case there are wiring differences between the practice robot and the competition robot.
