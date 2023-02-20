In order to set up an environment that allows us to test everything we need for the final demo, we need SITL to incorporate the following things:
- Run lua scripts
- Simulate or accepts commands to control servos and pwm
	- If this functionality is not directly implemented in SITL, maybe we can send messages to GC at the appropriate times and check manually
		- In this case, the tested program will do the following:
			1. Takeoff and fly to the bus
			2. Within a lua script, land and send a message from the script that indicates the drone is landed
			3. (Cannot wait for location to change without flying. Latching and unlatching will need to be tested IRL)
			4. Takeoff
			5. Fly to delivery location, land, move precision land arm, adjust servos to release package.
			6. Takeoff

# Resources
[Fixing Mission Planner SITL](https://discuss.ardupilot.org/t/simulation-in-mission-planner-complaining-about-missing-dll/94385/5) There is an issue where mission planner says cygwin is not installed
[Basic Example](https://dronekit-python.readthedocs.io/en/latest/examples/mission_basic.html)
[Dronekit missions documentation](https://dronekit-python.readthedocs.io/en/latest/guide/auto_mode.html)
[Index for ArduPilot missions documentation](https://ardupilot.org/copter/docs/common-mission-planning.html)
	- [Copter Mission Command List](https://ardupilot.org/copter/docs/mission-command-list.html)
	- Lots of the examples are in mission planner. Can I build it out from there then try to convert them to dronekit?
### [Script Calls into the firmware](https://ardupilot.org/copter/docs/common-scripted-aerobatics-4.4.html#script-calls-into-the-firmware "Permalink to this heading")
Other scripts can be developed which allow control of the vehicle, either via NAV_SCRIPT_TIME mission items or from normal flight modes. The key calls are:
-   Enabling scripting control override of roll/pitch/yaw rates and throttle with a specific call “vehicle:nav_scripting_enable(..)” which returns a boolean indicating success or failure.
-   Obtaining the arguments of a NAV_SCRIPT_TIME command using “vehicle:nav_script_time()” if running while in AUTO mode.
-   Controlling the above rates and throttle with the “vehicle:set_target_throttle_rate_rpy(….)” function, which must be called regularly (at least every second) to set the roll/pitch/yaw rates and throttle percentage. Failure to do so, will disable the control override and return control to the original flight mode. Changing flight modes also disables script control.