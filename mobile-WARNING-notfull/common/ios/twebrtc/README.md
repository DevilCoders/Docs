[__!__] Please report all WebRTC related (not specific to this binary build) bugs and questions to [discussion group](https://groups.google.com/forum/#!forum/discuss-webrtc) or [official bug tracker](https://bugs.chromium.org/p/webrtc/issues/list). You more likely to find professional help there.

# WebRTC SDK for iOS
This pod contains the WebRTC iOS SDK in binary form. It is a dynamic library
that contains the armv7, arm64 and x86_64 slices.
Bitcode is not supported.
Our currently provided API’s are Objective C only.

Chromium versions [List](https://chromiumdash.appspot.com/branches)

## Changes
1.0.0
- Chromium version m79

1.1.0
- Chromium version m91

### How to build artifact
1. Install chrome depot_tools - [guide](https://webrtc.github.io/webrtc-org/native-code/development/prerequisite-sw/)

2. Create folder and navigate to it in terminal
`cd ${PATH_TO_FOLDER}`

3. Fetch WebRTC ( and wait )
`fetch --nohooks webrtc_ios`

4. Synchronize gclient
`gclient sync --with_branch_heads --with_tags`

5. Navigate to src folder
`cd ./src/`

6. Checkout actual release branch
`git checkout -b branch_m74 branch-heads/m74`
Actual branch:
`Branch ID: m79`

7. Synchronize gclient ( again )
`gclient sync --with_branch_heads --with_tags`

8. Build .fat-framework
`python tools_webrtc/ios/build_ios_libs.py`

9. Validate framework
Framework will be at path - `/src/out_ios_libs/WebRTC.framework`
Validate archs ( should contain string `x86_64 i386 armv7 arm64` )
`lipo -info ${PATH_TO_FOLDER}/src/out_ios_libs/WebRTC.framework/WebRTC`

## Getting started
If you are new to WebRTC valuable resources can be found at webrtc.org/start/.
More documentation can be found at https://webrtc.org/native-code/ios/.
Sample code can be found [here](https://webrtc.googlesource.com/src/+/master/examples/objc/AppRTCMobile/).

## Notice
While WebRTC source code is licensed under BSD, it depends on many
other open sourced projects. The list of relevant transitive licenses are
enclosed in LICENSE.md.

## Terms of Service
WebRTC is a free, open project that provides browsers and mobile applications
with Real-Time Communications (RTC) capabilities via simple APIs. The WebRTC
components have been optimized to best serve this purpose.

Our mission: To enable rich, high-quality RTC applications to be developed for
browsers, mobile platforms, and IoT devices, and allow them all to communicate
via a common set of protocols.

The WebRTC Mobile libraries are part of Google’s effort to facilitate the
adoption of WebRTC on Android and iOS. They can be integrated with projects in
Apple’s Xcode and Android studio directly, giving developers the opportunity to
start experimenting with WebRTC. The libraries are published weekly as a
snapshot of the WebRTC source code at
https://webrtc.googlesource.com/src. They are targeted for
developers that want to try out WebRTC on mobile devices.

Thank you,
-The WebRTC Team
