fastlane documentation
================
# Installation

Make sure you have the latest version of the Xcode command line tools installed:

```
xcode-select --install
```

Install _fastlane_ using
```
[sudo] gem install fastlane -NV
```
or alternatively using `brew cask install fastlane`

# Available Actions
## iOS
### ios beta
```
fastlane ios beta
```
Yandex beta build
### ios unit_tests
```
fastlane ios unit_tests
```
Unit tests
### ios ui_tests
```
fastlane ios ui_tests
```
UI tests
### ios screenshots
```
fastlane ios screenshots
```

### ios build_appstore
```
fastlane ios build_appstore
```
Build for AppStore
### ios build_tests_for_simulator
```
fastlane ios build_tests_for_simulator
```
Build tests with scheme PowerDirect for a simulator
### ios build_tests_for_device
```
fastlane ios build_tests_for_device
```
Build tests with scheme PowerDirect for a device
### ios upload_latest_testplan_to_lpq
```
fastlane ios upload_latest_testplan_to_lpq
```
Upload latest testplan.zip to LPQ

----

This README.md is auto-generated and will be re-generated every time [fastlane](https://fastlane.tools) is run.
More information about fastlane can be found on [fastlane.tools](https://fastlane.tools).
The documentation of fastlane can be found on [docs.fastlane.tools](https://docs.fastlane.tools).
