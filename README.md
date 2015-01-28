!macdependency

Clone of http://code.google.com/p/macdependency/

This is an updated version that (should) compile on OSX 10.7 and later

Licence LGPL

MacDependency shows all dependent libraries and frameworks of a given executable, dynamic library or framework on Mac OS X. It is a GUI replacement for the otool command, and provides almost the same functionality as the Dependency Walker (http://www.dependencywalker.com) on Windows.

According to the author, macdependency 
dyld source code could be find here :


## Build

	git clone --recursive https://github.com/StudioEtrange/macdependency
	cd macdependency/MacDependency
	xcodebuild

MacDependency.app is now in macdependency/MacDependency/build/Release

## Usage

Launch MacDependency.app
Drag&Drop a .dylib file on MacDependency icon in the dock