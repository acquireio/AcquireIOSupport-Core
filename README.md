# AcquireIOSupport-Core
AcquireIO support (Core) for real time chat and audio/video call

This guide describes the process of implementing AcquireIOSupport Core SDK into your iOS app

We recommend using CocoaPods as the most advanced way of managing iOS project dependencies.

### Installation
To connect AcquireIOSupport Core SDK to your iOS app just add it into your Podfile:

1) Create a Podfile in your project's root directory, if it doesn't exist yet

2) Add the **AcquireIOSupport-Core** in Podfile under your desired target:

   ```

   target :YourTargetName do
      pod 'AcquireIOSupport-Core'
   end

   ```

3) The AcquireIOSupport SDK supports module stability and therefore all its dependencies must be built in with the "Build Libraries for Distribution" setting enabled, however this is not currently supported in Cocoapods. Running below command will ensure Xcode builds the dependencies with the correct settings. Once Cocoapods supports module stability, this workaround can be removed.

Add the following to the bottom of your Podfile: 

    ```

    post_install do |installer|
      installer.pods_project.targets.each do |target|
        if ['TwilioVideo', 'Socket.IO-Client-Swift', 'Starscream'].include? target.name
          target.build_configurations.each do |config|
              config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
              config.build_settings['ENABLE_BITCODE'] = 'NO'
          end
        end
      end
    end

    ```


4)  Run below command to install the SDK to your project 
        
      ```bash
  
      $ pod install --repo-update

     ```

5)  Open your project using the generated *.xcworkspace file.


>  ###   **Note:** If you are new to CocoaPods, go to [CocoaPods](https://cocoapods.org/) to learn how to install it.


Make sure to always open the Xcode workspace instead of the project file when building your project:


```
open YourTargetName.xcworkspace
```

### Setup Info.plist

>  *Since iOS 10, it's mandatory to add before you access privacy-sensitive data like Camera, Microphone, and so on, you must ask for the authorization, or your app will crash when you access them.*

Open the file in your project named info.plist, right click it, opening as Source Code, paste this code below to it. Or you can open info.plist as Property List by default, click the add button, Xcode will give you the suggest completions while typing Privacy - with the help of keyboard and

Remember to write your description why you ask for this authorization, between <string> and </string>, or your app will be rejected by apple:
```
<!-- Camera -->
<key>NSCameraUsageDescription</key>
<string>$(PRODUCT_NAME) use camera for video chat</string>

<!-- Microphone -->
<key>NSMicrophoneUsageDescription</key>
<string>$(PRODUCT_NAME) use microphone for voice chat</string>

<!-- Photo Library -->
<key>NSPhotoLibraryUsageDescription</key>
<string>$(PRODUCT_NAME) send photo/video to agent</string>

```

Also, The AcquireIOSupport SDK uses background mode Audio for when you are video/voice call to agent/visitor. If you have not enable then background voice will not work. When the UIBackgroundModes key contains the audio value, the system’s media frameworks automatically prevent the corresponding app from being suspended when it moves to the background

To allow your AcquireIOSupport SDK to play audio in background, Enable it using below steps
1) Select your project file in the Navigator of Xcode.
2) From the Capabilities section, switch on the **Background Modes** subsection
3) Switch **ON** the Background Modes subsection. After background modes are listed, tick on the *Audio, Airplay & picture in picture*

![Background Mode](https://s3.amazonaws.com/com.twilio.prod.twilio-docs/images/BackgroundModes.original.png)

## Setup and installation guide

* Our [installation guide](https://developer.acquire.io/v/2.0.0/sdk/ios/sdk-setup-guide/integration-guide-core) contains full setup and initialization instructions.


* Please contact us on [AcquireIO Support](https://acquire.io) with any questions you may have, we're only a message away!
