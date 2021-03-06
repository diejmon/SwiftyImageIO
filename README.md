# SwiftyImageIO

[![Swift](https://img.shields.io/badge/Swift-5.0-orange.svg)]()
[![SPM Ready](https://img.shields.io/badge/SPM-ready-orange.svg)](https://swift.org/package-manager/)
[![Version](https://img.shields.io/cocoapods/v/SwiftyImageIO.svg?style=flat)](http://cocoapods.org/pods/SwiftyImageIO)
[![License](https://img.shields.io/cocoapods/l/SwiftyImageIO.svg?style=flat)](http://cocoapods.org/pods/SwiftyImageIO)
[![Platform](https://img.shields.io/cocoapods/p/SwiftyImageIO.svg?style=flat)](http://cocoapods.org/pods/SwiftyImageIO)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)

Swift wrapper around ImageIO framework.

## Usage

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Examples


### Create image thumbnail

```swift
import SwiftyImageIO

let source = ImageSource(data: imageData, options: nil)
let thumbnailCGImage = source?.createThumbnail(maxPixelSize: thumbnailSize)
```

### Write image to disk

```swift
import SwiftyImageIO
import MobileCoreServices

if let imageDestination = ImageDestination(url: saveURL, UTI: kUTTypeJPEG, imageCount: 1) {
  imageDestination.addImage(cgImage)
  let imageSaved = imageDestination.finalize()
}
```

### Create GIF from animated UIImage

```swift
let gifMaker = GIF()
try gifMaker.makeGIF(fromAnimatedImage: animatedImage,
                     writeTo: savePath,
                     properties: GIF.Properties(loopCount: 1),
                     frameProperties: GIF.FrameProperties(delayTime: 0.1))
```

### Read GPS image properties

```swift
let source = ImageSource(url: jpgWithExifImageURL, options: nil)
guard let properties = source?.propertiesForImage() else {
  XCTFail("We created image without properties.");
  return
}
guard let gpsProperties = properties.get(GPSImageProperties.self) else {
  XCTFail("GPS Not available")
  return
}
```

### Test examples

[Test Examples](Example/Tests/Tests.swift)

## Installation

### CocoaPods

```ruby
pod "SwiftyImageIO"
```

### Swift Package Manager

```swift
dependencies: [
    .Package(url: "https://github.com/diejmon/SwiftyImageIO.git", majorVersion: 0, minor: 4)
]
```

### Carthage 

```ogdl
github "diejmon/SwiftyImageIO" ~> 0.4
```

### EXIF

The list of exif values can be found in this [document](https://www.exif.org/Exif2-2.PDF)

## Author

Alexander Belyavskiy, diejmon@gmail.com

## License

SwiftyImageIO is available under the MIT license. See the LICENSE file for more info.
