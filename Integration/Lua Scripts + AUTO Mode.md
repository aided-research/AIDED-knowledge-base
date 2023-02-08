*How can we compute flight plans form the GCS and have it flown on the drone with docking and undocking?*
[Parameters to Consider when using Lua scripts or Auto mode](https://ardupilot.org/copter/docs/parameters.html#wpnav-parameters)

# Missions (AUTO mode)
[Copter Mission Commadnd List](https://ardupilot.org/copter/docs/mission-command-list.html)
## Navigation Commands
*Affect the location of the vehicle*
Some that may be relevant:
- [LAND](https://ardupilot.org/copter/docs/mission-command-list.html#land) Command
- [Script Time](https://ardupilot.org/copter/docs/mission-command-list.html#script-time)
	- Calls a lua script for a specified amount of time. Allows three parameters to be passed


## Do Commands
*For auxiliary functions that do not affect the vehicle's position*
- [Delay](https://ardupilot.org/copter/docs/mission-command-list.html#delay). Specify seconds or UTC datetime
- [Condition Distance](https://ardupilot.org/copter/docs/mission-command-list.html#condition-distance). Delay a do command until within a certain distance
- [Do-Aux-Function](https://ardupilot.org/copter/docs/mission-command-list.html#do-aux-function) Can call several built in [functions](https://ardupilot.org/copter/docs/common-auxiliary-functions.html#common-auxiliary-functions) that are usually assigned to buttons on the controller.
	- ARM/DISARM and ARM/Motor Emergency Stop.
> [!INFO]
> The [AUTO_OPTIONS](https://ardupilot.org/copter/docs/parameters.html#auto-options) parameter can be used to allow arming/disarming while in AUTO mode, and/or, allowing a mission takeoff command to start upon AUTO mode entry, even if the throttle has not been raised.
- [Do-Set-Relay](https://ardupilot.org/copter/docs/mission-command-list.html#do-set-relay)  Set a [Relay](https://ardupilot.org/copter/docs/common-relay.html#common-relay) pin’s voltage high or low
- [Do-Gripper](https://ardupilot.org/copter/docs/mission-command-list.html#do-gripper). rip-n-grip


## Relevant Lua Code
[Fast Descent Lua Script](https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP_Scripting/examples/copter-fast-descent.lua)
- Shows how to create and bind variables to drone's parameters (Ctrl F "create and initialise parameters")
- Uses the idea of stages to control the steps in the script. Seems to be common in the examples

In this code, ```vehicle:nav_script_time()``` gets the paramters set in the command from the mission.
```auto_last_id``` seems to be the indication of if the script should run.
```lua
auto_last_id, cmd, arg1, arg2, arg3, arg4 = vehicle:nav_script_time()
if not arming:is_armed() or not auto_last_id then
  stage = 0
  if (update_user and arming:is_armed()) then
	gcs:send_text(6, "Fast Descent: waiting for NAV_SCRIPT_TIME")
  end
  return update, interval_ms
end
```

At the end of this script, the mission command can be marked as done
```lua
elseif (stage == 2) then  -- Stage2: done!
	stage = stage + 1
	gcs:send_text(5, "Fast Descent: done!")
	if (activate_type:get() == 0) then
	  -- if activated from Guided change to RTL mode
	  vehicle:set_mode(copter_rtl_mode_num)
	else
	  -- if activated from Auto NAV_SCRIPT_TIME then mark command as done
	  vehicle:nav_script_time_done(auto_last_id)
	end
end
```


# Matter of fact, where's everybody from?
*How can we get these things working together?*
Come back to this.


