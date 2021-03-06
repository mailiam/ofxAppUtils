ofxAppUtils
===========

OpenFrameworks app utilities

Copyright (c) [Dan Wilcox](danomatika.com) 2011-2012

BSD Simplified License.

For information on usage and redistribution, and for a DISCLAIMER OF ALL
WARRANTIES, see the file, "LICENSE.txt," in this distribution.

See Documentation on [Github](https://github.com/danomatika/ofxAppUtils) and the [OpenFrameworks Forum post](http://forum.openframeworks.cc/index.php/topic,5995.0.html).

OpenFrameworks is a cross platform open source toolkit for creative coding in C++.

[http://www.openframeworks.cc/](http://www.openframeworks.cc/)

Description
-----------

ofxAppUtils is a set of utilities for OpenFrameworks application development including:

* ofxApp: an ofBaseApp/ofxiPhoneApp extension with built in screen scaling, projection mapping transforms, quad warping, and an optional ofxControlPanel
* ofxScene: a mini ofBaseApp/ofxiPhoneApp for writing stand alone scenes
* ofxSceneManager: handles a list of scenes using a std::map
* ofxTransformer: open gl transformer for origin translation, screen scaling, mirroring, and quad warping
* ofxQuadWarper: an open gl matrix quad warper (useful for oblique projection mapping)
* ofxTimer: a simple millis-based timer
* ofxParticle: a simple time-based particle base class
* ofxParticleSystem: an auto manager for ofxParticles
* ofxBitmapString: a stream interface for ofDrawBitmapString

All ofBaseApp & ofxiPhoneApp callbacks are handled down to the scene level.

Installation
------------

To use ofxAppUtils, first you need to download and install Open Frameworks. ofxAppUtils is currently developed against the latest stable version of Open Frameworks on github.

To get a copy of the repository you can download the source from [http://github.com/danomatika/ofxAppUtils/zipball/master](http://github.com/danomatika/ofxAppUtils/zipball/master) or, alternatively, you can use git clone:
<pre>
git clone git://github.com/danomatika/ofxAppUtils.git
</pre>

The addon should sit in `openFrameworks/addons/ofxAppUtils/`.

You will may also need the following addon dependencies:

* ofxXmlSettings: included with OpenFrameworks (optional)
* ofxControlPanel: https://github.com/kylemcdonald/ofxControlPanel (optional, also requires ofxXmlSettings)

To disable the control panel (and ofxControlPanel dependency), define `OFX_APP_UTILS_NO_CONTROL_PANEL` in your CFLAGS.
To disable the xml transform load/save (and ofxXmlSettings dependency), define `OFX_APP_UTILS_NO_XML` in your CFLAGS.

For Xcode, see the example project Project.xcconfig files on how to set the defines.

Running the Example Project
-------------------------------

The example projects are in the `appUtilsExample` & `appUtilsIOSExample` folders.

### OSX

Xcode3: Open the Xcode project and hit "Build and Run". You might want to choose "Release" instead of "Debug" for faster performance.

Xcode4: Open the Xcode project, select the appUtilsExample-Debug scheme, and hit "Run".

### Linux

Open the Code::Blocks .cbp and hit F9 to build. Optionally, you can build the example with the Makefile.

To run it, use the terminal:
<pre>
make
cd bin
./example_debug
</pre>

### Windows

An example Visual Studio 2010 solution as well as a Codeblocks workspace are included.


Adding ofxAppUtils to an Existing Project
---------------------------------------

If you want to add ofxAppUtils to another project, you need to make sure you include the src folders:
<pre>
openFrameworks/addons/ofxAppUtils/src
</pre>

### Xcode

* create a new group "ofxAppUtils"
* drag these directories from ofxAppUtils into this new group: ofxAppUtils/src
* you also need to add the following addon dependencies in a similar manner:
	* ofxControlPanel
	* ofxXmlSettings
	
On iOS you will probably want to disable the control panel via the `OFX_APP_UTILS_NO_CONTROL_PANEL` define as it is doesn't really work with touch screens.

### For Linux (Makefiles & Codeblocks):

* edit addons.make in your project folder and add the following line to the end of the file: 
	<pre>ofxAppUtils</pre>
* edit config.make in your project folder and update the USER_CFLAGS line if you want to disable the control panel and/or xml saving:
	<pre>
	USER_CFLAGS = -DOFX_APP_UTILS_NO_CONTROL_PANEL -DOFX_APP_UTILS_NO_XML
	</pre>
	
### For Codeblocks (Win):

* add the ofxAppUtils sources to the project:
	* right-click on your project in the project tree
	* select "Add Files Recursively ..."
	* navigate and choose the ofxAppUtils/src folder
* add defines, search paths, and libraries to link:
	* right-click on your project in the project tree
	* select "Build options..."
	* make sure the project name is selected in the tree (not release or debug)
	* select the "Compiler settings" tab, add the following to the "#defines" tab if you want to disable the control panel and/or xml saving:
	<pre>
	OFX_APP_UTILS_NO_CONTROL_PANEL
	OFX_APP_UTILS_NO_XML
	</pre>
	* select the "Search directories" tab, click add the search paths:
	<pre>
	..\\..\\..\addons\ofxAppUtils\src
	</pre>

### Extending Your BaseApp

There are two changes you need to make to extend your app with the ofApputils ofxApp class which handles all the *automagic*:

* your base app needs to inherit from ofxApp in your testApp.h
<pre>
class testApp : public ofBaseApp { 
// becomes
class testApp : public ofxApp { 
</pre>
* you need to run your app with the app utils in main.cpp
<pre>
ofRunApp(new testApp());
// becomes
ofRunAppWithAppUtils(new testApp());
</pre>

That's it. Check the example testApp::setup() for more info on startup settings.

Note: this is completely optional. You can always handle the transforms etc yourself using an ofxTransformer instance, etc.

DEVELOPING
----------

You can help develop ofxAppUtils on GitHub: [https://github.com/danomatika/ofxAppUtils](https://github.com/danomatika/ofxAppUtils)

Create an account, clone or fork the repo, then request a push/merge.

If you find any bugs or suggestions please log them to GitHub as well.
