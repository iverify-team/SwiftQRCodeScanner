# WARNING
This fork is modified to specifically work in our iVerify mobile EDR solution and isn't intended to be used as-is by
the general public.  Some references to external files may be present and attempting to use this project as is without
the external files may result in failure to compile.

All modified files are clearly indicated in the copyright notice at the top of every file.

Changes include visual appearance to better fit with the styling of our app and references to image assets.



# SwiftQRCodeScanner
![QR Scanner](https://user-images.githubusercontent.com/30258541/170007055-763fda9a-3edd-4d11-99c9-04f3d3067e8a.gif)

## Features
- Easy to use
- Customize everything
- Scan QR Code from saved photos

## Screenshots
| Without camera and flash | With camera and flash |
| ------ | ------ |
| <img src="https://user-images.githubusercontent.com/30258541/169960154-a1c4770d-a3df-412c-9064-85abdcbe1ac8.jpeg">  | <img src="https://user-images.githubusercontent.com/30258541/169960286-143ba622-0ce2-4252-9d3c-be450641546c.jpeg">  |


## Example
To run the example project, clone the repo, go to Example folder and open SwiftQRScanner.xcworkspace.

## Requirements
- iOS 10.0
- Xcode 11.0+
- Swift 5

## Installation
### Using CocoaPods
SwiftQRScanner is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'SwiftQRScanner', :git => ‘https://github.com/vinodiOS/SwiftQRScanner’
```
### Swift Package Manager Installation
Swift Package Manager
```ruby
dependencies: [
    .package(url: "https://github.com/vinodiOS/SwiftQRCodeScanner.git", from: "1.1.6")
]
```

### Manual Installation
Download the latest version ,then unzip & drag-drop the Classes  folder inside your iOS project. You can do that directly within Xcode,
just be sure you have the **copy items if needed** and the **create groups** options checked.

### Do you want to use SwiftQRCodeScanner with SwiftUI?
Please follow this example [QRCodeSwiftUIExample](https://github.com/vinodiOS/QRCodeSwiftUIExample).

## How to use
Import SwiftQRScanner module and confirm to the QRScannerCodeDelegate protocol.

```Swift
import SwiftQRScanner

class ViewController: UIViewController {
}

extension ViewController: QRScannerCodeDelegate {
}
```

Create instance of SwiftQRScanner to scan QR code.
```Swift
let scanner = QRCodeScannerController()
scanner.delegate = self
self.present(scanner, animated: true, completion: nil)
```
To use more features like camera switch, flash and many other options use **QRScannerConfiguration**:
```Swift
var configuration = QRScannerConfiguration()
configuration.cameraImage = UIImage(named: "camera")
configuration.flashOnImage = UIImage(named: "flash-on")
configuration.galleryImage = UIImage(named: "photos")

let scanner = QRCodeScannerController(qrScannerConfiguration: configuration)
scanner.delegate = self
self.present(scanner, animated: true, completion: nil)
```
And finally implement delegate methods to get result:
```Swift
func qrScanner(_ controller: UIViewController, didScanQRCodeWithResult result: String) {
    print("result:\(result)")
}

func qrScanner(_ controller: UIViewController, didFailWithError error: SwiftQRCodeScanner.QRCodeError) {
    print("error:\(error.localizedDescription)")
}

func qrScannerDidCancel(_ controller: UIViewController) {
    print("SwiftQRScanner did cancel")
}
```

Complete code:
```Swift
import UIKit
import SwiftQRScanner

class ViewController: UIViewController {
        
    @IBAction func scanQRCode(_ sender: Any) {
    
        //Simple QR Code Scanner
        let scanner = QRCodeScannerController()
        scanner.delegate = self
        self.present(scanner, animated: true, completion: nil)
    }
    
    @IBAction func scanQRCodeWithExtraOptions(_ sender: Any) {
        
        //Configuration for QR Code Scanner
        var configuration = QRScannerConfiguration()
        configuration.cameraImage = UIImage(named: "camera")
        configuration.flashOnImage = UIImage(named: "flash-on")
        configuration.galleryImage = UIImage(named: "photos")
        
        let scanner = QRCodeScannerController(qrScannerConfiguration: configuration)
        scanner.delegate = self
        self.present(scanner, animated: true, completion: nil)
    }
    
}

extension ViewController: QRScannerCodeDelegate {    
    func qrScanner(_ controller: UIViewController, didScanQRCodeWithResult result: String) {
        print("result:\(result)")
    }
    
    func qrScanner(_ controller: UIViewController, didFailWithError error: SwiftQRCodeScanner.QRCodeError) {
        print("error:\(error.localizedDescription)")
    }
    
    func qrScannerDidCancel(_ controller: UIViewController) {
        print("SwiftQRScanner did cancel")
    }
}
```

You can use following **QRScannerConfiguration** properties:

| Property Name | Default Value | Description |
| ------ | ------ |------ |
| title | "Scan QR Code" | Title of SwiftQRCodeScanner |
| hint | "Align QR code within frame to scan" | Hint for QR Code scan suggestion |
| uploadFromPhotosTitle | "Upload from photos" | Button title for pick QR Code from saved photos |
| invalidQRCodeAlertTitle | "Invalid QR Code" | Title for Alert if invalid QR Code |
| invalidQRCodeAlertActionTitle | "OK" | Title for Action if invalid QR Code |
| cameraImage | nil | Image for camera switch button |
| flashOnImage | nil | Image for flash button |
| length | 20.0 | Length of QR Code scanning frame |
| color | green | Color of QR Code scanning frame |
| radius | 10.0 | Corner Radius of QR Code scanning frame |
| thickness | 5.0 | Corner Thickness of QR Code scanning frame |
| readQRFromPhotos | true | Hide/show "Upload From photos" button|
| cancelButtonTitle | "Cancel" | Title for cancel button |
| cancelButtonTintColor | nil | Color for cancel button |
| hideNavigationBar| false | Hide/show navigation bar |

## Author

Vinod, vinod.jagtap@hotmail.com

## License

SwiftQRScanner is available under the MIT license. See the LICENSE file for more info.

