---
author: rogermolas
comments: true
date: 2015-04-10 06:00:00+00:00
layout: post
link: https://rogermolas.wordpress.com/2015/04/10/ios-dependency-management/
slug: ios-dependency-management
title: iOS Dependency Management
wordpress_id: 7
categories:
- CocoaPods
- Dependency
- iOS
- ruby
---

As an iOS developer, you certainly use a third-party libraries or a source code made by others to extend your app’s abilities. At first, it seems easy, just drag and drop some source code or libraries in your Xcode project or drag and drop an entire subproject into the parent project and you are done.

Just imagine how difficult it would be if you had to implement everything from scratch!

However, this has several disadvantages:



	
  * There’s no central place where you can see all your third party libraries that are available.

	
  * It's difficult to find the updated version of the library you used especially if several libraries need to be updated together.

	
  * Third party libraries is wasting space in your project.

	
  * If the subproject is updated by its owner, your code is out of date.


A dependency management tool called **[CocoaPods](https://cocoapods.org/)** can help you to solve these issues.


## Installing CocoaPods


CocoaPods is installed through RubyGems, a package management system for Ruby programming language, which comes with a standard OS X install.

To install CocoaPods

[code language="bash"]
$ sudo gem install
[/code]

Complete the setup of CocoaPods environment

[code language="bash"]
$ pod setup
[/code]


## Installing Dependency


Navigate to the directory containing your App project

[code language="bash"]
$ cd ~/Path/Directory/Folder/App
[/code]

Next enter this command

[code language="bash"]
$ pod init
[/code]

This will create a default Podfile for your project.
Podfile should look like this

[code language="bash"]
# Uncomment this line to define a global platform for your project
# platform :ios, '6.0'$ pod install
target 'App' do

end
[/code]

A **[Podfile](http://guides.cocoapods.org/syntax/podfile.html)** is where the dependencies of a project are listed.

Add dependency in Podfile
CocoaPods follows **[Semantic Versioning](http://semver.org/)** conventions

[code language="bash"]
pod 'AFNetworking', '2.5.1'
[/code]
This tells CocoaPods that you want to include AFNetworking version 2.5.1 as a dependency for your project.

Once all of the dependencies have been specified, they can be installed with the following command

[code language="bash"]
$ pod install
[/code]

CocoaPods will recursively analyze the dependencies of each project, resolving them into a dependency graph, and serializing into a Podfile.lock file. Podfile.lock keeps track of dependencies version need to be installed.


### Created files


**_Pods directory_** - where all dependencies are stored.

**_xcworkspace_** - should be used from that point onward. This allows the original xcodeproj file to remain unchanged.

CocoaPods will create a new Xcode project that creates static library targets for each dependency, and then links them all together into a _libPods.a_ target.

Subsequent invocations of pod install will add new pods or remove old pods according to the locked dependency graph.

Update the individual dependencies of a project

[code language="bash"]
$ pod update
[/code]
Understanding what’s happening behind the scenes can only help you make better apps.

We’ve walked through the entire process, from installing tools, adding sources, creating the .xcodeproj and all its components, to writing everything to disk.

So next time, run the following command and watch the magic happen.

[code language="bash"]
$ pod install --verbose
[/code]


## Wrapping Up


CocoaPods is one example of the great work being done on Objective-C infrastructure. And its goal is to improve the discoverability of, and engagement in, third-party open-source libraries. And it's only getting better.


To know more, read through the **[CocoaPods Guides](http://guides.cocoapods.org/)** for finer details of using CocoaPods.
