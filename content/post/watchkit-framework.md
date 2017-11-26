---
title: "WatchKit Framework"
date: 2015-05-13 10:14:00+00:00
draft: false
categories: [Apple Watch, WatchKit]
tags: [iOS,WatchKit]
author: rogermolas
---

WatchKit is the new framework created by Apple for Apple Watch development, WatchKit is available starting Xcode 6.2 and iOS 8.2.

Analogous to UIKit for iOS apps, the framework allows developers to drop in custom interfaces and interact with your existing iOS app.

When app is launched on Apple Watch, the WatchKit extension on iPhone runs in the background to update the user interface and respond to user interactions.

WatchKit framework provides three opportunities to extend your iPhone app to Apple Watch: WatchKit app, Glances, and actionable Notifications. While Glances and Notifications are optional.

WatchKit only supports two basic types of navigation methods, hierarchical style and page-based style.

**Hierarchical style** applications have an implicit navigational stack, which WKInterfaceController can manage with_ **"pushControllerWithName:context:"**_** & "**_**popController"**._

**Page-based style** application is a paginated interface where users can swipe horizontally between pages of information.

Here are some API’s


### WKInterfaceController


WKInterfaceController manages the elements in a scene, whereas UIViewController manages a view and its subviews.

```
override init(context: AnyObject?) {
   super.init(context: context)
    // ...
}
```

It has a designated initializer method that accept optional context object, context is anything you want e.g string, date, numbers or nothing at all.

```
override func willActivate() {
   super.willActivate()
    // ...
}
```

```
override func didDeactivate() {
   super.didDeactivate()
    // ...
}
```
All setup for the interface controller's scene like initialization of elements, properties and any objects is to be done in the initializer and **_"willActivate"_ **method. Both during and after **_"didDeactivate"_** method, the Watch will ignore attempts to update the state of interface elements.


### WKInterfaceObject


WKInterfaceObject is the base class for all interface objects, an interpretation of UIView where you can manipulate elements display with properties for alpha, hidden, and width & height.


### WKInterfaceButton


WKInterfaceButton is an interface object that can be tapped to trigger an action, this is interpretation of UIButton. Its contents can be either a text, an optional background color, image or a group.


### WKInterfaceTable


WKInterfaceTable object creates and manages the contents of a single-column table interface an interpretation of UITableView in iOS.

Compared to UITableView, WKInterfaceTable do not have sections, headers and footers, editing style, searching, data sources and delegates. Rows are pre-populated at -willActivate method. WKInterfaceController can respond to table interactions with the **_table:didSelectrowAtIndex:_** delegate method, or using target-action method.

Rows in WKInterfaceTable need to specify its own row controller (an NSObject subclass with IBOutlets).


### WKInterfaceLabel


WKInterfaceLabel support NSAttributedString, custom fonts, and font scaling. Least-changed thing carried over from iOS.


### WKInterfaceTimer


WKInterfaceTimer special type of label that displays a countdown until a specified date.


### WKInterfaceDate


WKInterfaceDate special type of label that displays the current date or time.


### WKInterfaceSlider & WKInterfaceSwitch


WKInterfaceSlider visual representation for the range of values and WKInterfaceSwitch visual representation for On and Off state. Both controls is customizable.

Imagine the earliest days of iOS development, when the platform limitations acted as liberating constraints for developers no arc, no .xcassets, no storyboard, apps were simple, small, and humble. After 7 years iOS has grown to extremely great number of devices from iPod Touch to iPhones and iPads, Apple TV. Its still an amazing developer experience.


### Conclusion


WatchKit is a new exciting framework for developers to think of new ways to provide interactivity and best user experience in Apple Watch. Apple provided enough resources and references to build quite a complex yet functional apps for Apple Watch.

Watch kit and Apple Watch is something to be enjoyed and celebrated.


### Reference:


**[The best way to get started](https://developer.apple.com/watchkit/)**
**[Human interface Guidelines](https://developer.apple.com/watch/human-interface-guidelines/)**
**[WatchKit programming guide](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/index.html)**
**[Sample code demonstrates how to use UI elements available in the WatchKit framework.](https://developer.apple.com/library/prerelease/ios/samplecode/WKInterfaceCatalog/Introduction/Intro.html)**
[**Adding Apple Watch app extension in your existing app(Objective-C & Swift).**](https://developer.apple.com/library/prerelease/ios/samplecode/Lister/Introduction/Intro.html)
