---
title: "Grand Central Dispatch and Swift 3"
date: 2016-12-09 10:43:00+00:00
draft: false
categories: [GCD, Swift3, Threading]
tags: [GCD, Swift3, Multi-Threading]
author: rogermolas
---

**[Grand Central Dispatch](https://developer.apple.com/reference/dispatch) **(GCD or libdispatch) a system level library for managing concurrent operations develop by Apple Inc., it is one of the more complicated and unfriendly APIs in iOS SDK. It was written in C programming language using this API felts like writing low-level C code that executed directly into hardware.

GCD or libdispatch is a combination of logic in the xnu kernel alongside the user-space library. The kernel has the most information available to balance workload across the entire system.

GCD manages FIFO queues to which your application can submit tasks in the form of block objects (dispatch queue). Each task object can be executed either synchronously or asynchronously.

One of the most common GCD patterns is to perform work on a global background queue and update the UI on the main queue as soon as the work is done.


### Objective-C

```
dispatch_queue_t backgroundQueue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_BACKGROUND, 0);
dispatch_async(backgroundQueue, ^{
  UIImage *parsedImage = [UIImage imageWithData:data]  // backround task
  dispatch_async(dispatch_get_main_queue(), ^{
     [self displayImage:parsedImage];                  // update UI
  });
});
```


### Swift 2.x

```
let qosClass = QOS_CLASS_BACKGROUND
let backgroundQueue = dispatch_get_global_queue(qosClass, 0)
dispatch_async(backgroundQueue, {
   let parsedImage = UIImage(data: data)              // backround task
   dispatch_async(dispatch_get_main_queue(), ^{
      self.display(image: parsedImage)               // update UI
   });
});
```

Both ObjectiveC and Swift(older version) first create the service class by using **DISPATCH_QUEUE_PRIORITY_BACKGROUND**, **QOS_CLASS_BACKGROUND**,  then create the background queue by using system call **dispatch_get_global_queue **which returns instance of **dispatch_queue_t** and pass it to **dispatch_async** call.

As you can see, its not a pure Swift and Objective-C syntax because it is exposed directly from libdispach library which is written in C programming language.


### New Swift 3.0 dispatch syntax


Swift 3.0 introduce a new set of data structures and models for Grand Central dispatch.

**DispatchQueue** Class enables creating and modifying queues, dispatching synchronously or asynchronously and etc..

```
DispatchQueue.global(qos: .background).async {
   let parsedImage = UIImage(data: data)        // backround task
   DispatchQueue.main.async {
      self.display(image: parsedImage)          // update UI
   }
}
```

Quality of service is replaces the old priority attributes that were deprecated in iOS8.

```
* DISPATCH_QUEUE_PRIORITY_HIGH:        .userInitiated
* DISPATCH_QUEUE_PRIORITY_DEFAULT:     .default
* DISPATCH_QUEUE_PRIORITY_LOW:         .utility
* DISPATCH_QUEUE_PRIORITY_BACKGROUND:  .background
```

Some of the queues that we use are already present as DispatchQueue instance

Creating queue using default initializer

```
let queue = DispatchQueue(label: "com.process.queue")
```

Dispatch using the main thread (_dispatch_get_main_queue()_)

```
DispatchQueue.main.async {
   print("main thread dispatch")
}

```
**DispatchWorkItem - **wrap a block of code and pass it to **DispatchQueue**

```
let workItem = DispatchWorkItem(qos: .userInitiated, flags: .assignCurrentContext) {
   // Do work here
}
queue.async(execute: workItem)
```

**Dispatch After**

```
DispatchQueue.main.asyncAfter(deadline: .now() + 5.0) {
  // Task invoke after 5 seconds
}
```

**Dispatch assert**

```
let queue = DispatchQueue.global(qos: DispatchQoS.QoSClass.default)
let mainQueue = DispatchQueue.main
mainQueue.async {
dispatchPrecondition(condition: .notOnQueue(mainQueue))
   // This code won't execute
}
queue.async {
dispatchPrecondition(condition: .onQueue(queue))
   // This code will execute
}
```

**dispatchPrecondition** replace dispatch_assert and allow you to check whether or not you are on the expected thread before executing code.

In Swift 3, **dispatch_once** is deprecated, it should be replace with either global, static and constants variables.


### Conclusion


GCD new APIs bring more flexibility and easy way to get things done,  although its still in beta and **[_documentation_](https://developer.apple.com/reference/dispatch/dispatchqueue)** is still incomplete.


