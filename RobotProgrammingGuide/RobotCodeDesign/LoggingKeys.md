# LoggingKeys

Within mechanisms, we log various details about a mechanism’s state to make it easier to set tuning constants and to debug hardware and software issues on the robot. Where this information is sent depends on the robot’s configuration, but typically it can be viewed in the Smart Dashboard running on the Driver Station laptop while the robot is running. The `LoggingKey` enumeration contains the list of every piece of information that is logged during operation, along with the corresponding names displayed in the log or on the dashboard.
