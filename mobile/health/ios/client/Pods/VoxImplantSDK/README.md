# Voximplant iOS SDK

![](https://img.shields.io/cocoapods/v/VoxImplantSDK.svg?maxAge=100) ![](https://img.shields.io/cocoapods/dw/VoxImplantSDK.svg?maxAge=100)
![](https://img.shields.io/cocoapods/l/VoxImplantSDK.svg?maxAge=100)

Voximplant iOS SDK lets you embed voice communication into your native iOS applications. It is a framework
that contains the armv7, arm64, i386 and x86_64 slices.
Bitcode is __disabled__.

You can make and receive calls using your device’s data connection to/from any other endpoint that works with Voximplant: other mobile app built using Voximplant Mobile SDK, web application built using the Web SDK, SIP phones and phone numbers all over the world.

# Contents

- [Installation](#installation)
- [Usage](#usage)
- [Links](#links)
- [License](#LICENSE)

# Installation

You can install Voximplant iOS SDK via CocoaPods:

Add this line to your `Podfile`
```ruby
pod "VoxImplantSDK"
```

Then run `pod install`

# Usage

## Swift
```swift
import VoxImplant

let client = VIClient(delegateQueue: DispatchQueue.main)
```

## Objective-C
```objc
@import VoxImplant;

VIClient *client = [[VIClient alloc] initWithDelegateQueue:dispatch_get_main_queue()];
```

Check out [Example App](https://github.com/voximplant/ios-sdk-swift-demo) for implementation.

# Links

[Quick Start](http://voximplant.com/docs/quickstart/25/using-ios-sdk/)

[Documentation](http://voximplant.com/docs/references/mobilesdk/ios/)

[Changelog](http://voximplant.com/docs/references/mobilesdk/ios/changelog/index.html)

# LICENSE

Copyright (c) 2011-2018, Zingaya, Inc.
All rights reserved.

Redistribution and use in binary forms, without modification, is permitted provided that the following conditions are met:

1. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

2. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
