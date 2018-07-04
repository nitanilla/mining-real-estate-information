Distributed UI Framework
========================

The goal of this project is to provide a framework that developers can use to create a unified application that runs
concurrently across multiple devices.  This is not a cross platform framework like qt, but something akin to a hybrid
message passing / shared memory parallel programming system. This framework is intended to allow developers to easily
create applications that can spread their user interfaces across multiple iOS and MacOS devices, while maintaining 
common development patterns like MVC, delegation, and KVO. Ultimately we would like to provide a nearly seamless 
development pattern in which the developer can create storyboards for multiple and concurrent executing devices that 
may be automatically integrated and removed from existing application sessions. The  framework exposes additional 
simplified  functionality for distributed computing by sharing data across the network interface.

Integrating into the Application
--------------------------------

* Add the DistributedUI.framework for Mac or iOS to your project.
* Use `@import DistributedUI` to source files that should interact with the DUI system.
* Use the `SYNTHESIZE_SHARED_SINGLETON()` macro to register shared instances of your main controller classes, or register shared objects directly.
* Start a DUISession. Hosts advertise their presence on the network interface and a client browsers for connections

	```
	[[DUIManager sharedDUIManager] startDistributedInterfaceHostSession];
		... or ...
	[[DUIManager sharedDUIManager] startDistributedInterfaceClientSession];
	```

* Establish a connection using MCBrowserViewController.
* When connection is made the DUIPeerDidConnect noitification is sent out.  Dismiss the browser.  You're now runnning
  a distributed application session.

Development Notes
-----------------

* Guidelines for copying mutable and immutable objects are generally inverted for DUI sessions.  Because utable objects are subject to change they are not safe to copy remotely where a change might not be propogated. An immutable object can be safely copied and stored remotely since it is gauranteed to remain consistent.
* Design components in such a way as to facilitate UI extensions. E.g., move controls into view controllers instead of toolbars.  This will let your application use more real estate for the document content.

Todo
----

* Add a custom pairing view controller and/or make the pairing process less interactive.  Also provide an automatic connection option.
* Add method decorators (e.g., DUI_NONBLOCKING, DUI_BLOCKING, etc), that serve to declare methods as supported under DUI and to control their behaviour.
* Add unit test coverage for all foundation classes and types.
* Add better exceptions and errors.
* Add NSApplication extensions.  Make the DUI session more like a single 'app'.
* We are currently running without any security of any kind.    o_O
* Add support for remote KVO
* Add categories/method swizzles on NSObject and NSNotification center to support /automatic/ remote registration of key and notification observers.
* Work towards a less client-host and more peer-to-peer model.
* Flip the connect model.  It makes more sense for clients to advertise and hosts to invite them to sessions.

Examples
--------

Note: testing the example projects will require at least two device, and at least two iPads/iPhones for the DUIDraw example.  To use the examples, build and install the test application on one or more devices, the use the host / connect options to pair the devices. 

### DUIDraw

This example multiple iOS devices to create a distributed paint application.  When multiple devices are present in the application session the user interface is distributed across all devices.  When one device is present the application uses a traditional 'toolbar' based interface.

![DUIDraw Screen Shot](https://cloud.githubusercontent.com/assets/450207/7334723/ebd0bb70-eb4f-11e4-89ed-41519b6d7c41.gif)

### DUIChess

The chess example implements a simple multiplayer game using multiple devices.  The app supports any combination of up to 8 iPhone, iPad, and Mac devices.

![DUIChess Screen Shot](https://cloud.githubusercontent.com/assets/450207/7334724/ec047046-eb4f-11e4-8b73-79477509d085.gif)


Copyright & Acknowledgements
----------------------------

Copyright (C) Caleb C. Cannon 2015
