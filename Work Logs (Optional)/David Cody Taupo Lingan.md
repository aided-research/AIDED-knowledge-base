## 2/6/23
### Summary:
* 





## 2/5/23

### Summary:
* Team Meeting
* Setting up SITL + FlightGear 3D View to visualize flights

### Blockers: 
* SITL + FlightGear 3D View may or may not be for MacOS; documentation of SITL does not explicitly mention that SITL + FlightGear 3D is possible, yet downloading SITL and FlightGear alone on MacOS is possible. Mixed messages man.
* After vimming into an sh file that represents an arduPilot vehicle in `/ardupilot/Tools/autotest`,  such as  `fg_plane_view.sh` , this command `nice` can be found in each file, which gives this error: `<insert error>` . This is my main blocker. To recreate this error, [somewhat follow these steps](https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html#), running any MacOS equivalent steps to non-MacOS functionalities.

### Links:
https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html#

https://wiki.flightgear.org/New_to_FlightGear#:~:text=If%20you%20would%20like%20to,cd%20%2FApplications%2FFlightGear ?

https://discuss.ardupilot.org/t/sim-vehicle-py-command-not-found/37184/2