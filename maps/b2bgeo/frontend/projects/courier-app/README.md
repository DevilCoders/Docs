This project was bootstrapped with [Create React Native App](https://github.com/react-community/create-react-native-app).

Below you'll find information about performing common tasks. The most recent version of this guide is available [here](https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md).

## Table of Contents

- [Launching App](#launching)
  - [Run on Android device](#run-on-android-device)
  - [Run on iOS device](#run-on-ios-device)
- [Updating to New Releases](#updating-to-new-releases)
- [Available Scripts](#available-scripts)
- [Writing and Running Tests](#writing-and-running-tests)
- [Customizing App Display Name and Icon](#customizing-app-display-name-and-icon)
- [Permissions](#permissions)
- [Troubleshooting](#troubleshooting)
  - [Networking](#networking)
  - [When running on Android](#when-running-on-android)
  - [When running on iOS](#when-running-on-ios)
  - [QR Code does not scan](#qr-code-does-not-scan)

## Launching

### **Run on Android device**

#### What is necessary?

1. Java (we recommend installing it via brew):

for example

```sh
brew install --cask adoptopenjdk8
```

2. Android Studio

3. ADB (Android Debug Bridge):

```sh
brew install android-platform-tools
```

Сonfiguring https://developer.android.com/studio/command-line/adb#Enabling

After setting up, you can see the connected device

```sh
$ adb devices

List of devices attached
{DEVICE_ID}	device
```

#### Running by wire on a real device

1. We connect the phone by wire to the computer (you need to give consent to trust the computer, etc.) and we go into the same wifi network with him.
2. Configuring ports

```sh
npm run ports:android
```

3. Build js and install the app on your phone

```sh
npm run dev:android
```

#### Wiki

[https://wiki.yandex-team.ru/users/edgarnurullin/android-dev/](https://wiki.yandex-team.ru/users/edgarnurullin/android-dev/)

### **Run on iOS device**

1. Install pod
   https://guides.cocoapods.org/using/getting-started.html

2. Install the necessary dependencies

```
cd ios
pod install
```

3. Build js at the root of the project:

```
npm run build:ios
```

(we get the main.bundle file + assets folder)

4. Register AppleID in Xcode settings

#### Running on the emulator

1. Open the XCode folder of the ios project

2. Select the emulator for which to build (to the right of the play button)

3. Start the build (press the play button)

P.S. tested on iPod v1.9.3, macOS Catalina 10.15.7, Xcode 12.0.1, iPhone simulator 11

Teamcity:
https://teamcity.yandex-team.ru/project/Mobile_B2bgeoCourierApp?mode=builds

[https://wiki.yandex-team.ru/users/edgarnurullin/build-react-native-ios-app/](https://wiki.yandex-team.ru/users/edgarnurullin/build-react-native-ios-app/)

## Updating to New Releases

You should only need to update the global installation of `create-react-native-app` very rarely, ideally never.

Updating the `react-native-scripts` dependency of your app should be as simple as bumping the version number in `package.json` and reinstalling your project's dependencies.

Upgrading to a new version of React Native requires updating the `react-native`, `react`, and `expo` package versions, and setting the correct `sdkVersion` in `app.json`. See the [versioning guide](https://github.com/react-community/create-react-native-app/blob/master/VERSIONS.md) for up-to-date information about package version compatibility.

## Available Scripts

If Yarn was installed when the project was initialized, then dependencies will have been installed via Yarn, and you should probably use it to run these commands as well. Unlike dependency installation, command running syntax is identical for Yarn and NPM at the time of this writing.

### `npm run ports:android`

Configuring ports

```sh
adb reverse tcp:8081 tcp:8081 && adb reverse tcp:8080 tcp:8080
```

### `npm run dev:android`

Build js and install the app on your phone

### `npm test`

Runs the [jest](https://github.com/facebook/jest) test runner on your tests.

## Customizing App Display Name and Icon

You can edit `app.json` to include [configuration keys](https://docs.expo.io/versions/latest/guides/configuration.html) under the `expo` key.

To change your app's display name, set the `expo.name` key in `app.json` to an appropriate string.

To set an app icon, set the `expo.icon` key in `app.json` to be either a local path or a URL. It's recommended that you use a 512x512 png file with transparency.

## Writing and Running Tests

This project is set up to use [jest](https://facebook.github.io/jest/) for tests. You can configure whatever testing strategy you like, but jest works out of the box. Create test files in directories called `__tests__` to have the files loaded by jest. See the [the template project](https://github.com/react-community/create-react-native-app/tree/master/react-native-scripts/template/__tests__) for an example test. The [jest documentation](https://facebook.github.io/jest/docs/getting-started.html) is also a wonderful resource, as is the [React Native testing tutorial](https://facebook.github.io/jest/docs/tutorial-react-native.html).

## Permissions

If you want to get the full list of permissions

### For Android

https://stackoverflow.com/questions/21091022/listing-permissions-of-android-application-via-adb/21091023#21091023

- 1) You need to get the `.apk` file (you can take it from any task)
- 2) You need to run the command
```sh
aapt d permissions path/to/your.apk
```
In my case, the shell could not find the `aapt` module, in which case you will need to specify the full path to the `aapt` executable file, in my case it was this path *`~/Library/Android/sdk/build-tools/32.0.0/aapt`*

For example:
```sh
~/Library/Android/sdk/build-tools/32.0.0/aapt d permissions path/to/your.apk
```

## Troubleshooting

### Networking

If you're unable to load your app on your phone due to a network timeout or a refused connection, a good first step is to verify that your phone and computer are on the same network and that they can reach each other. Create React Native App needs access to ports 19000 and 19001 so ensure that your network and firewall settings allow access from your device to your computer on both of these ports.

Try opening a web browser on your phone and opening the URL that the packager script prints, replacing `exp://` with `http://`. So, for example, if underneath the QR code in your terminal you see:

```
exp://192.168.0.1:19000
```

Try opening Safari or Chrome on your phone and loading

```
http://192.168.0.1:19000
```

and

```
http://192.168.0.1:19001
```

If this works, but you're still unable to load your app by scanning the QR code, please open an issue on the [Create React Native App repository](https://github.com/react-community/create-react-native-app) with details about these steps and any other error messages you may have received.

If you're not able to load the `http` URL in your phone's web browser, try using the tethering/mobile hotspot feature on your phone (beware of data usage, though), connecting your computer to that WiFi network, and restarting the packager.

### When running on Android

> `Could not initialize class org.codehaus.groovy.reflection.ReflectionCache`

[Stack Overflow](https://stackoverflow.com/questions/60844245/how-solve-could-not-initialize-class-org-codehaus-groovy-reflection-reflectionc)

```sh
export JAVA_HOME="/Applications/Android Studio.app/Contents/jre/jdk/Contents/Home"
```

> `SDK location not found. Define location with an ANDROID_SDK_ROOT environment variable`

[Stack Overflow](https://stackoverflow.com/questions/40248265/how-to-set-android-sdk-root-in-mac)

```sh
export ANDROID_SDK_ROOT=~/Library/Android/sdk
```

> `You have not accepted the license agreements of the following SDK components`

[Stack Overlfow](https://stackoverflow.com/questions/39760172/you-have-not-accepted-the-license-agreements-of-the-following-sdk-components)

> `Could not initialize class org.codehaus.groovy.runtime.InvokerHelper`

[Stack Overflow](https://stackoverflow.com/questions/35000729/android-studio-could-not-initialize-class-org-codehaus-groovy-runtime-invokerhel)

> `java.nio.file.NoSuchFileException: courier-app\android\app\build\intermediates\externives\debug\out`

[Github](https://github.com/facebook/react-native/issues/28954)

### When running on iOS

> `iOS Simulator won't open`

If you're on a Mac, there are a few errors that users sometimes see when attempting to `npm run ios`:

- "non-zero exit code: 107"
- "You may need to install Xcode" but it is already installed
- and others

There are a few steps you may want to take to troubleshoot these kinds of errors:

1. Make sure Xcode is installed and open it to accept the license agreement if it prompts you. You can install it from the Mac App Store.
2. Open Xcode's Preferences, the Locations tab, and make sure that the `Command Line Tools` menu option is set to something. Sometimes when the CLI tools are first installed by Homebrew this option is left blank, which can prevent Apple utilities from finding the simulator. Make sure to re-run `npm/yarn run ios` after doing so.
3. If that doesn't work, open the Simulator, and under the app menu select `Reset Contents and Settings...`. After that has finished, quit the Simulator, and re-run `npm/yarn run ios`.

### QR Code does not scan

If you're not able to scan the QR code, make sure your phone's camera is focusing correctly, and also make sure that the contrast on the two colors in your terminal is high enough. For example, WebStorm's default themes may [not have enough contrast](https://github.com/react-community/create-react-native-app/issues/49) for terminal QR codes to be scannable with the system barcode scanners that the Expo app uses.

If this causes problems for you, you may want to try changing your terminal's color theme to have more contrast, or running Create React Native App from a different terminal. You can also manually enter the URL printed by the packager script in the Expo app's search bar to load it manually.

---

### Debug

```
./gradlew installDebug
npm start
adb reverse tcp:8081 tcp:8081
adb reverse tcp:8080 tcp:8080
```

номер курьера из flash logistic - 102-2

### Release

```
npm version minor
./gradlew assembleRelease
node ./upload.js
```

### integration tests

all integration test code is located in the `api-tests/` folder

configs for tests are located in the folder `api-tests/config`
the config `default.js` is overwritten by the selected environment `testing.js` or `production.js`

### run integration tests

checkout latest version master 0. сlone repository

```
git clone https://github.yandex-team.ru/B2BGeo/ya-courier-app.git
```

1. install dependencies

```
npm i
```

2. run tests

for testing env

```
SUPER_USER_TOKEN=AAA APP_USER_TOKEN=AAA UNREGISTERED_USER_TOKEN=AAA CONFIG=testing npm run api-tests
```

for production env

```
SUPER_USER_TOKEN=AAA APP_USER_TOKEN=AAA UNREGISTERED_USER_TOKEN=AAA CONFIG=production npm run api-tests
```

`SUPER_USER_TOKEN` - it is OAuth token from passport user with super user rights. You could make yourself token. [instruction](https://yandex.ru/routing/doc/delivery/concepts/quickstart/register.html). Or [get it](https://yav.yandex-team.ru/secret/sec-01ddnqnfh237cr58aggnrknxfm/explore/versions) from robot

`APP_USER_TOKEN` - it is token from passport user with role APP. You could get it from [yav](https://yav.yandex-team.ru/secret/sec-01dwyqk288qevvtc0kdwp87a1b/explore/version/ver-01dz1g4wppcbwse92z7cmhbbrr)

`UNREGISTERED_USER_TOKEN` - it is token from passport user who isn't registered in ya backend. You could get it from [yav](https://yav.yandex-team.ru/secret/sec-01ed9eqmfxdhdn7xqn46shcfwm)

### I18n

We are using **Tanker**. Details in `.tanker/readme.md`

#### iOS

We are using tanker **`native-ios`** keyset, and write translations to **`[Locale ID].lproj/InfoPlist.strings`**

> [Locale ID] = ru/en/tr ...etc

```sh
npm run i18n:ios
```

##### How to create new locale file

XCode > yandex.courier > PROJECT > Info > Localizations

#### Android

Android translations generated by writing `native-android` keyset into `(values|values-{ru/tr})/strings.xml`

```sh
npm run i18n:android
```

### Persist Migrations

1. Migrations are executed one by one. From persisted version (`state._persist.version`) to current version which comes from **PersistConfig**
2. If you have something that need to be transformed before being persisted/hydrated, then use **createTransform**. See `modules/api`, `modules/app`
3. If you upgraded version, do not forget to add state snapshot to fixtures with new test cases

### Why application might crash without appropriate migration

It might not be obvious at first.
First of all we persist some store slices in AsyncStorage using redux-persist.

1. Therefore if you will add new nested structure expecting that it will be required (in terms of TS),
   application might rehydrate using persisted state and here your expectations might not match and application would crash.
2. You will rename/change some nested structure, and again updated code might not expect persisted state to be different.



