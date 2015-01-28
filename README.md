#macdependency

Clone of http://code.google.com/p/macdependency/

This is an updated version that (should) compile on OSX 10.7 and later

Licence LGPL

MacDependency shows all dependent libraries and frameworks of a given executable, dynamic library or framework on Mac OS X. It is a GUI replacement for the otool command, and provides almost the same functionality as the Dependency Walker (http://www.dependencywalker.com) on Windows.




## Build

	git clone --recursive https://github.com/StudioEtrange/macdependency
	cd macdependency/MacDependency
	xcodebuild

MacDependency.app is now in macdependency/MacDependency/build/Release

## Usage

* Launch MacDependency.app
* Drag&Drop a .dylib file on MacDependency icon in the dock

## Search Path of Library

According to the author, macdependency is built on dyld doc and analysis of dyld 97.1 source code
Main logic of is in dyld.cpp method
	ImageLoader* load(const char* path, const LoadContext& context)

dyld doc : https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/dyld.1.html
dyld source code : http://www.opensource.apple.com/source/dyld/ OR http://www.opensource.apple.com/tarballs/dyld/

NOTE : Maybe macdependency should be updated with an analysis of last version of dyld

ORIGINAL POST : https://code.google.com/p/macdependency/wiki/SearchPaths

Details
First of all the dependent filename is stripped, so that only the filename without any path information is extracted. Then the dyld tries to find the file in different directories in the following order. As soon as the file is found, the mechanism terminates:

* find filename in all paths given by LD_LIBRARY_PATH (separated by ":")
* if filename is a framework: find framework name (without path information) in all paths given by DYLD_FRAMEWORK_PATH (separated by ":")
* find filename in all paths given by DYLD_LIBRARY_PATH (separated by ":")
* if filename starts with @executable_path, @loader_path or @rpath those strings are replaced by the path of the current executable, the path of the binary which depends on this file or the given RPATHs (see http://www.mikeash.com/pyblog/friday-qa-2009-11-06-linking-and-install-names.html)
* find filename (including original path information)
* if filename is a framework: find framework name (without path information) in all paths given by DYLD_FALLBACK_FRAMEWORK_PATH (separated by ":"). If this environment variable isn't set, it instead looks in the following default paths: ~/Library/Frameworks,/Library/Frameworks,/Network/Library/Frameworks,/System/Library/Frameworks
find filename in all paths given by DYLD_FALLBACK_LIBRARY_PATH (separated by ":"). If this environment variable isn't set, it instead looks in the following default paths: ~/lib,/usr/local/lib,/lib,/usr/lib