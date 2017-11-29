---
title: "New iOS9 String Transformations API"
date: 2015-06-29 09:44:00+00:00
draft: false
categories: [Strings, NSStringTransform]
tags: [iOS,CFString]
author: rogermolas
---

String transformations formerly done using CFStringTransform a part of Core Foundation Framework. In iOS 9 string transformation can be done along with the new _“_**_NSStringTransform*_**_”_ constants a native Cocoa API and no need to deal with bridging to **_CFStringRef_**.

Here are some of my favorite transformations that can be done with the new NSStringTransform* API.

```
print("roger".stringByApplyingTransform(NSStringTransformLatinToGreek, reverse: false)!)
//ῤογερ
print("roger".stringByApplyingTransform(NSStringTransformLatinToHangul, reverse: false)!)
//로겔
print("\uD83D\uDC2E".stringByApplyingTransform(NSStringTransformToUnicodeName, reverse: false)!)
//{COW FACE}
```
