# Open Source Driver Station (OSDS)

This app is an open-source version of the FTC 2015-16 Driver Station app in the Play Store.  It is based off of the beta Driver Station source code distributed to teams at preview events. I combined it with the up-to-date backend libraries taken from the FTC SDK, as well as some decompiled bits of the Play Store Driver Station code to create a modified driver station which works with the current Robot Controller app.


### Code Ownership
The GUI source code in this was written by Qualcomm and modified by me.  It is still their property.  Other libraries are from Qualcomm's open source FTC code, and from the OpenRC project.

### Pros & Cons
#### Why you WOULD use this driver station
- It supports a larger range of devices and screen sizes than the default app (though it won't magically fix Wifi Direct on devices where it is broken or not present)
- It gives you quite a bit more screen real estate for Telemetry, depending on the size of your device's screen
- It allows you to customize your team's DS.  You can do simple color and icon theming, or something as complicated as parsing the Telemetry feed and creating a GUI for your robot.
- It supports LAN mode (see below).
- It features a much less jarring and aggressive "Configuring Wifi, please wait..." dialog, which hopefully won't get stuck in a loop.  All this is doing is toggling wifi off and on anyway.

#### Why you WOULDN'T use this driver station
- I have NO IDEA if it is at all competition legal, or will work at competition.  Make sure to keep a supported driver station device for competition use.
- It may be buggier than the official DS, as the GUI was not originally meant to work with this version of the backend library.
- Maybe you really like the official DS's color scheme?

### Download
Check the releases section at the top.

### LAN Mode
LAN mode is an alternate method of connecting the robot controller and the driver station.  It connects through a router over WiFi instead of over Wifi Direct, which lets you connect to the robot simply by joining the phones to the same wifi network and typing in the IP address of the controller on the DS. In my experience, it connects far more quickly and robustly then the wifi direct version, and hardly ever requires anything to be rebooted or restarted (yay!).  Since it uses a regular wifi network, you can use Android's network debugging with ease, and even (double yay!) download and run a robot controller program without you ever having to touch the robot controller phone.
 
LAN mode does require modifications to your robot controller code, though.  Currently, I am working with the OpenFTC project to integrate these changes into OpenRC.  Stay tuned!

### Screenshot
![Screenshot](https://app.box.com/shared/static/55yjju2ataxzut0wqy7k5nmui1pdgknu.png)
