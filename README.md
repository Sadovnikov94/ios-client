# MathpixClient

[![Platform](http://img.shields.io/badge/platform-ios)](https://developer.apple.com/resources/)
[![Language](https://img.shields.io/badge/swift-3.0-orange.svg)](https://developer.apple.com/swift)

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Installation

#### CocoaPods

MathpixClient is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "MathpixClient", :git => 'https://github.com/Mathpix/ios-client.git', :tag => '0.0.1'
```

## Usage

First set api keys:

```swift
MathpixClient.setApiKeys(appId: "mathpix", appKey: "139ee4b61be2e4abcfb1238d9eb99902")
```

You can use MathpixClient to recognize images:

```swift
MathpixClient.recognize(image: UIImage(named: "equation")!, outputFormats: [FormatLatex.simplified]) { (error, result) in
    print(result ?? error)
}
```

MathpixClient can launch camera controller to capture and recognize images:

```swift
MathpixClient.launchCamera(source: self,
                           outputFormats: [FormatLatex.simplified],
                           completion:
            { (error, result) in
                  self.outputTextView.text = result.debugDescription + "  " + (error?.localizedDescription ?? "")
            })
```
You can fine tune this camera controller using `MathCaptureProperties` instance:

```swift
let properties = MathCaptureProperties(captureType: .gesture,
                                               requiredButtons: [.flash, .back],
                                               cropColor: UIColor.green,
                                               errorHandling: true)
        
        // Launch camera with back and completion blocks
        MathpixClient.launchCamera(source: self,
                                   outputFormats: [FormatLatex.simplified],
                                   withProperties: properties,
                                   completion:
            { (error, result) in

        })

```

If you need more control, you can subclass `MathCaptureViewController`. See example project to more info.


