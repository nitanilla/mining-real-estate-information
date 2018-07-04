# Smart Power Control
	Smart Power Control is an Android App for controlling switchable outlets
	like the ANEL NET-series (http://www.anel-elektronik.de)

You can find a ready to install apk at [Github Releases](https://github.com/davidgraeff/Android-NetPowerctrl/releases)
and on [Google Play](https://play.google.com/store/apps/details?id=oly.netpowerctrl).
For bugs and feature requests please use [Github Issues](https://github.com/davidgraeff/Android-NetPowerctrl/issues).

## Features
* Devices are detected automatically on the network.
* Username/password and individual ports can be configured for every device.
* Use your own icons for on/off/unreachable widget states.
* Combine multiple switch actions into a "scene". Master/Slave configurations are supported. Use own icons for scenes.
* Create a homescreen widget for a particular outlet/scene or a list of outlets and always see the current state of that outlet, master/slave scene or list of outlets/scenes.
* Overview of all outlets for all configured devices. Assign actions to specific view groups (for example "bedroom", "living room") and switch easily with a swipe between view groups.
* Create homescreen shortcuts for scenes. Shortcuts can be used by other applications (automation apps) to control your outlets.
* Dark and light app theme.
* Tablet layout included to use your screen real estate efficiently.
* Outlets and IO ports of Anel devices are supported.
* Plugin support. With plugins you can control additional related functionality for your needs.

<table><tr valign="top">
<td><img width="120px" src="doc/outlets-v600.png" /></td>
<td><img width="120px" src="doc/outlets-big_icons-v600.png" /></td>
<td><img width="120px" src="doc/devices-v600.png" /></td>
<td><img width="120px" src="doc/viewmode-v600.png" /></td>
<td><img width="120px" src="doc/widgets-v600.png" /></td>
</tr></table>

### Automatic device detection
Devices are detected automatically if they are configured for UDP communication.
Default send port 1077 / receive port 1075. Please be aware that you cannot use port numbers < 1024 as receive ports because of security restrictions!

### Support for automation apps like Tasker/Llama
Most of the automation apps support shortcuts of other applications.
Because a shortcut of this app refers to a scene, you may easily switch multiple
outlets as an action within an automation app.

Cool examples:
* This way you can for instance switch on lights if your mobile gets in range of your wifi network.
* You may turn on your amplifier or radio and some lights in the morning.

### Building
To compile, you need the [Android SDK](http://developer.android.com/sdk)
and [Android Studio](http://developer.android.com/sdk/installing/studio.html).
This project is not for the old eclipse based SDK! It depends on the
support libraries (v13), additional support library extensions (v7.RecyclerView) and need at least android 4.2 (sdk version 17, released 13. Nov 2012). Parts of the app (import/export/backgrounds) are only usuable with Android 4.4 (DocumentProvider class).

### Plugin Development
In ealier versions plugins via the android IPC were supported. This is no longer the case. Your app will be started by NetPowerCtrl via a Broadcast, from this point on, use the simpleUDP protocol for communication.
All you need to develop a plugin is described in detail at the [Plugin Developer Documentation](https://github.com/davidgraeff/Android-NetPowerctrl/blob/master/doc/simpleudp.md). Sample implementations are available here: https://github.com/davidgraeff/esp8266_dev/tree/master/app_pc

### Authors
* david.graeff(at)web_de
* Some icons from http://www.clker.com/

### Used external libraries
* com.github.rey5137:material:1.1.0 (Apache License, Version 2.0)
* com.wefika:flowlayout:0.3.4 (Apache License, Version 2.0)
* jp.wasabeef:recyclerview-animators:1.2.0@aar (Apache License, Version 2.0)
* com.github.gabrielemariotti.changeloglib:library:1.5.2 (Apache License, Version 2.0)
* ch.acra:acra:4.6.2 (Apache License, Version 2.0)
* net.lingala.zip4j:zip4j:1.3.2 (Apache License, Version 2.0)
* com.google.code.ndef-tools-for-android:ndeftools:1.2.4 (Apache License, Version 2.0)
    
### License
Dual licensed: GPLv2+GPLv3
