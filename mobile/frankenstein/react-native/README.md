# react-native-frankenstein

## Getting started

`$ npm install react-native-frankenstein --save`

### Android

1. Add yandex artifactory:
```groovy
maven { url 'https://artifactory.yandex.net/mobile' }
maven { url 'https://artifactory.yandex.net/yandex_mobile_snapshots' }
```
2. Add `classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.3.61"` to buildscript.
3. Add to the Application.onCreate():
```kotlin
val mockHostsFunction = getUrlUpdater(applicationContext, MOCK_HOST_RULES_FILE)
URL.setURLStreamHandlerFactory(MockHostUrlStreamHandlerFactory(mockHostsFunction))
```

For included logs, add to the `Application.onCreate()`:
```kotlin
Timber.plant(Timber.DebugTree())
```

### iOS

1. Add to Podfile:
```ruby
pod 'YXTFrankenstein', :path => "#{MONOREPO_ROOT}/frankenstein/ios/"
```

For included logs, add to the `application:didFinishLaunchingWithOptions:`:
```Objective-C
[YXTUtils enableLogging];
```

### Mostly automatic installation

`$ react-native link react-native-frankenstein`

## Usage
1. Add import in index.js:
```javascript
import Frankenstein from 'react-native-frankenstein';
```
2. Add in index.js after `AppRegistry.registerComponent(appName, () => App);`
```javascript
Frankenstein.requestTestCase(testCaseParameters => {
  const env = testCaseParameters.environment;
  Frankenstein.runTestCase(env, env.mockHostRules);
});
```
