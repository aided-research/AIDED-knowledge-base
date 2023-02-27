
## 2/26/23
* Calling Lua scripts within ArduPilot missions - how does an ArduPilot mission know that a Lua script is done?
	* Because we're working with hardware, it's our responsibility to provide feedback as to when a Lua script is done. 

## 2/19/23
### Summary:
* In ArduPilot missions, how do you control servos (gripper - also a servo depedning on how you setup in ArduPilot)
* How can we do this in DroneKit?
* * [This the answer](obsidian://open?vault=AIDED-knowledge-base&file=Integration%2FDroneKit%20%2B%20Servos)


* Calling Lua scripts within ArduPilot missions - how does an ArduPilot mission know that a Lua script is done?



## 2/13/23
### Summary:
* Move day to new lab :(
* Team Meeting
* Currently editting proposal

### Blockers:
* SITL is not for MacOS M1 chips. As for MacOS systems prior to M1, probably works.
* Why?
* [For MacOS, the only option to run SITL](https://ardupilot.org/dev/docs/setting-up-sitl-using-vagrant.html) is to use a virtual machine setup, which hinges on separate software, [Vagrant](https://developer.hashicorp.com/vagrant/downloads) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads). 
* This is where some confusion is introduced, but bare with me:
	* The most recent version of VirtualBox (7.0.6) is the only version compatible with M1 Macs.
	* Vagrant and VirtualBox work together to setup the virtual machine. However, Vagrant can [only work with versions of VirtualBox that is not 7.0.6.](https://developer.hashicorp.com/vagrant/docs/providers/virtualbox) Hopefully you see why this option does not work.
	* Why did this case arise? Because the VirtualBox (7.0.6) version came out just late January of this year (2023) to accomodate M1 Macs, however Vagrant has yet to do the same.

### Future:
* Setting up a testing environment should be done on a device that is not MacOS. I am positive that setting this up on another device won't take long.




## 2/10/23
### Summary:
* First proposal design meeting! 
* Read over whole proposal. 
* Sat in the hallway >:)


## 2/8/23
### Summary:
* Will test [SITL + Vagrant](https://ardupilot.org/dev/docs/SITL-setup-landingpage.html), which I'm told is compatible on MacOS.
* Pivoting to working on ImaginAviation for today - address simulation later.

### Blockers:
* After running `vagrant up` per instructions of [this page](https://ardupilot.org/dev/docs/setting-up-sitl-using-vagrant.html), I receive 
```
The guest machine entered an invalid state while waiting for it

to boot. Valid states are 'starting, running'. The machine is in the

'aborted' state. Please verify everything is configured

properly and try again.

  

If the provider you're using has a GUI that comes with it,

it is often helpful to open that and watch the machine, since the

GUI often has more helpful error messages than Vagrant can retrieve.

For example, if you're using VirtualBox, run `vagrant up` while the

VirtualBox GUI is open.

  

The primary issue for this error is that the provider you're using

is not properly configured. This is very rarely a Vagrant issue.
```

Always check for version compatibility between two applications before installing.

* SITL specifically is just not friendly towards M1 macs. the only option available to MacOS itself is the "SITL + Vagrant" option here: [https://ardupilot.org/dev/docs/SITL-setup-landingpage.html](https://ardupilot.org/dev/docs/SITL-setup-landingpage.html "https://ardupilot.org/dev/docs/SITL-setup-landingpage.html") long story short, Vagrant is only compatible with VirtualBox versions 6.1 and below. But VirtualBox versions that are not 7.0 is not compatible with M1 Macs (per this screenshot) I will try another alternative to SITL from that list you sent me brady to simulate an arduVehicle.

### Links
* https://ardupilot.org/dev/docs/SITL-setup-landingpage.html





## 2/6/23
### Summary:
* Confirmed that SITL + FlightGear 3D View is [not compatible on MacOS](https://discuss.ardupilot.org/t/tutorial-for-running-sitl-simulator-on-macos-with-vagrant-xquartz/38383) - should work for other OS if anyone wants to test.







## 2/5/23

### Summary:
* Team Meeting
* Setting up SITL + FlightGear 3D View to visualize flights

### Blockers: 
* SITL + FlightGear 3D View may or may not be for MacOS; documentation of SITL does not explicitly mention that SITL + FlightGear 3D is possible for MacOS, yet downloading SITL and FlightGear alone on MacOS is possible. Mixed messages man.
* After vimming into an sh file that represents an arduPilot vehicle in `/ardupilot/Tools/autotest`,  such as  `fg_plane_view.sh` , this command `nice` can be found in each file, which gives this error: `<insert error>` . This is my main blocker. To recreate this error, [somewhat follow these steps](https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html#), running any MacOS equivalent steps to non-MacOS functionalities.

### Links:
https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html#

https://wiki.flightgear.org/New_to_FlightGear#:~:text=If%20you%20would%20like%20to,cd%20%2FApplications%2FFlightGear ?

https://discuss.ardupilot.org/t/sim-vehicle-py-command-not-found/37184/2