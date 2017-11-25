---
author: rogermolas
comments: true
date: 2015-06-29 09:44:00+00:00
layout: post
link: https://rogermolas.wordpress.com/2015/06/29/new-ios9-string-transformations-api/
slug: new-ios9-string-transformations-api
title: New iOS9 String Transformations API
wordpress_id: 5
categories:
- iOS
- NSString
---

String transformations formerly done using CFStringTransform a part of Core Foundation Framework. In iOS 9 string transformation can be done along with the new _“_**_NSStringTransform*_**_”_ constants a native Cocoa API and no need to deal with bridging to **_CFStringRef_**.

Here are some of my favorite transformations that can be done with the new NSStringTransform* API.

[code language="objc"]
print("roger".stringByApplyingTransform(NSStringTransformLatinToGreek, reverse: false)!)
//ῤογερ

print("roger".stringByApplyingTransform(NSStringTransformLatinToHangul, reverse: false)!)
//로겔
print("\uD83D\uDC2E".stringByApplyingTransform(NSStringTransformToUnicodeName, reverse: false)!)
//{COW FACE}

[/code]
