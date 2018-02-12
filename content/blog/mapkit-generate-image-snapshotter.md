---
title: "Generate MapView Snapshot with Snapshotter"
date: 2018-02-12T14:29:02+08:00
draft: false
categories: [MKMapSnapshot, MapKit]
tags: [MKMapSnapshot, MapKit, Swift4]
author: rogermolas
---

[`MKMapSnapshotter`](https://developer.apple.com/documentation/mapkit/mkmapsnapshot) is use in creating an image representation of a map view. Previously, other developers use [`UIGraphicsContext`](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CocoaDrawingGuide/GraphicsContexts/GraphicsContexts.html), but now images can reliably be created for any particular region and perspective.

### Creating a Map View Snapshot
```
let mapSnapshotOptions = MKMapSnapshotOptions()
mapSnapshotOptions.region = mapView.region
mapSnapshotOptions.scale = UIScreen.main.scale
mapSnapshotOptions.size = mapView.frame.size
mapSnapshotOptions.showsBuildings = true
mapSnapshotOptions.showsPointsOfInterest = true

let snapShotter = MKMapSnapshotter(options: mapSnapshotOptions)
snapShotter.start { (snap, error) in
    let image = snap?.image
    imageView.image = image
}
```
According to Apple's [MKMapSnapshot](https://developer.apple.com/documentation/mapkit/mkmapsnapshot) doc

> Snapshot images do not include any custom overlays or annotations that your app added to the map view. If you want your annotations and overlays to appear on the final image, you must draw them yourself.


### Draw Stroke Color In Image

```
let image = snap?.image
UIGraphicsBeginImageContextWithOptions((image?.size)!, true, (image?.scale)!)
image?.draw(at: CGPoint(x: 0, y: 0))

let context = UIGraphicsGetCurrentContext()
context!.setStrokeColor(UIColor.blue.cgColor)
context!.setLineWidth(2.0)
context!.beginPath()

for (index, location) in locations.enumerated() {
    let coordinates = CLLocationCoordinate2DMake(location.latitude, location.longitude)
    let point = snap?.point(for: coordinates)
    if index == 0 {
        context?.move(to: point!)
    } else {
        context?.addLine(to:point!)
    }
}
context?.strokePath()
let finalImage = UIGraphicsGetImageFromCurrentImageContext()
UIGraphicsEndImageContext()
imageView.image = finalImage
```
The stroke color are rendered separately. By using `point(for:)`  it converts the specified map coordinate to a point in the coordinate space of the map image.



