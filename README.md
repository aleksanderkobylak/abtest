# AudioburstPlayer iOS SDK

## Introduction

AudioburstPlayer is the SDK for iOS that will let you play your previously prepared playlist of bursts.

## Features

AudioburstPlayer consists of two modes of audio player - compact (mini or floating) and fullscreen which allows you to:
- download a custom playlist,
- play any burst from the playlist,
- skip to the next or previous burst,
- switch to original listening,
- move backward and forward within a single burst,
- preview the title, the show name,
- play the playlist continuously in a background,
- control the playlist from the locked screen,
- plug the headphones or cast the audio to other devices via bluetooth or air-play,
- see bursts list,
- support dark/light theme.


<p align="middle">
<img src="screenshots/floating_player_1.png?raw=true"  width="200" hspace="5" title="Floating player"/><img src="screenshots/floating_player_2.png?raw=true"  width="200" hspace="5" /><img src="screenshots/mini_player.png?raw=true"  width="200" hspace="5" /><img src="screenshots/fullscreen_player.png?raw=true"  width="200" />
</p>


## Requirements

- iOS 12.0+
- Xcode 11

## Get Started

This guide is a quick start to add AudioburstPlayer to an iOS app. You can use [CocoaPods](http://cocoapods.org/) to install [AudioburstPlayer](https://cocoapods.org/pods/AudioburstPlayer). The AudioburstPlayerDemo application is a showcase of the AudioburstPlayer.


## Prerequisites

### Audioburst API key
Your application needs an **application key** (check [Audioburst Studio site](https://studio.audioburst.com/) to obtain the key).
Also you need to provide **experience id** that represents customized playlist settings (check [Audioburst Studio site](https://studio.audioburst.com/) to obtain the id)

## Add AudioburstPlayer to your app

### Step 1. Add AudioburstPlayer dependency
You can use [CocoaPods](http://cocoapods.org/) to install [AudioburstPlayer](https://cocoapods.org/pods/AudioburstPlayer) by adding it to your `Podfile`:

```ruby
platform :ios, '12.0'
use_frameworks!

target 'MyApp' do
    pod 'AudioburstPlayer', '~> 0.1.3'
end
```

### Step 2. Init AudioburstPlayer

Valid **application key** and **experience id** are needed to initialize player.

```swift
import AudioburstPlayer
```

```swift
let player = ABPlayer(appKey: "YOUR_APP_KEY", experienceId: "YOUR_EXPERIENCE_ID")
```

### Step 3. Loading Audioburst content
You simply need to call one method to load Audioburst content and get compact player view controller. Depending on mode set in Audioburst Studio, you will get floating player or mini player view controller Recommended view container size is: height `100 points`, width: `full screen width` )


```swift
player.load() { [weak self] result in
    if case let .success(viewController) = result {
        self.addViewControllerAsChild(viewController, parentView: self.playerViewContainer)
    }
}
```

### Step 4. Handle errors
`AudioburstPlayerError` enum is used to represent errors occured in AudioburstPlayer. To handle errors make your class implement `AudioburstPlayerErrorListener` protocol, for example:

```swift
extension ViewController: AudioburstPlayerErrorListener {
    func onError(error: AudioburstPlayerError) {
         self.showAlert(withTitle: "Error", message: error.localizedDescription)
    }
}
```
And add error listener for player:

```swift
player.add(errorListener: self) 
```

Please remember about unregistering error listener:

```swift
player.remove(errorListener: self)
```

### Step 5. Handle player events
To handle player events make your class implement `AudioburstPlayerListener` protocol, for example:

```swift
extension ViewController: AudioburstPlayerListener {
    func onClose() {
        removeViewControllerAsChild(compactPlayerVC)
    }
}
```
And add listener for player:

```swift
player.add(playerListener: self) 
```

Please remember about unregistering listener:

```swift
player.remove(playerListener: self)
```

## Dependencies
Libraries used by AudioburstPlayer (installed as pods dependencies)

- `Alamofire`
- `SwiftGen`
- `IBPCollectionViewCompositionalLayout`
- `Cache`
- `lottie-ios`
- `SDWebImage`
- `OwlKit`


## Privacy Policy
[Privacy Policy](https://audioburst.com/privacy)

## Terms of Service 
[Terms of Service](https://audioburst.com/audioburst-publisher-terms)

