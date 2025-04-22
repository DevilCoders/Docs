# Glagol Android SDK

```
GLAGOL -- Glagol is Location And Governance Over LAN
```

This SDK provides capabilities to connect and control YandexIO devices.
See https://st.yandex-team.ru/QUASAR-1625 / https://st.yandex-team.ru/QUASAR-1626

## New API usage (ConnectionDiscovery)

Main entry point is the `ru.yandex.quasar.glagol.Connector` interface's API.

Core entities are:
* `Connector` -- initializes all the processes, receives configuration on constructor
* `ConnectionDiscovery` - a process that scans local network, requests known ip-addresses and creates connections to user's available devices
* `LiveConnection` - established communication wrapper that handles reconnecting to different ips by itself

## How to use it

1. Acquire a `Connector` implementation, for example, instantiating the `ru.yandex.quasar.glagol.impl.ConnectorImpl` class, passing it required static configuration (e.g. backend hostnames and stuff, implementation-specific). A `Connector` instance is thread-safe.
2. When desired, start connection discovery process via `Connector#discoverConnections(Context, String, ConnectionDiscoveryListener)` call. It will return a `ConnectionDiscovery` instance which represents an ongoing process of device discovery and establishing connections to available devices. 
3. When new connection is established `ConnectionDiscoveryListener` will be notified with a `LiveConnection` object, representing an established two-way communication channel to the device chosen (and holds resources, like sockets). 
4. A `ConnectionDiscovery` should be closed when it is not needed via `close()` call.
5. `LiveConnection` objects should also be closed via `close()` call when no more communication is to be carried out.
6. If new `ConnectionDiscovery` is created it will create new instances of connections (if last ConnectionDiscovery-result connections were not closed)

## Old API usage (Manual discovery and connections establishment)
Main entry point is the `ru.yandex.quasar.glagol.Connector` interface's API.

Core entities are:
* `Connector` -- initializes all the processes, receives configuration on constructor
* `Discovery` -- a process of discovery, notifies callbacks of the discovered devices
* `Conversation` -- an established communication with a particular device

Follow the javadoc to get exact info.

## How to use it

1. Acquire a `Connector` implementation, for example, instantiating the `ru.yandex.quasar.glagol.impl.ConnectorImpl` class, passing it required static configuration (e.g. backend hostnames and stuff, implementation-specific). A `Connector` instance is thread-safe.
2. When desired, start a discovery process via `Connector#discover(Context, String, DiscoveryListener)` call. It will return a `Discovery` instance which represents an ongoing process of discovery. When a suitable device is discovered on LAN the `DiscoveryListener` passed to `discover(..)` call will be notified with a `DiscoveryResult` that contains a `DiscoveryResultItem` representing particular device. `DiscoveryResultItem`s are meant to represent particular device and should be persistable. A `Discovery` should be closed when it is not needed via `close()` call. `Connector#discover` is intended for general use.
3. Discovery process started via `Connector#discoverAll(Context, String, DiscoveryListener)` call will notify `DiscoveryListener` with devices found on LAN, just like `Connector#discover` but will also include devices that are not deemed accessible with given OAuth `token`.
Developer devices can skip certificate validation and connect to device without knowing it's certificate if needed using special socket.relaxsslcheck android property. see https://developer.android.com/reference/android/net/SSLCertificateSocketFactory
4. When a particular device is deemed worthy of being connected to start a particular device connection via `Connector#connect(DiscoveryResultItem, String, MessageListener)` call. It returns a `Conversation` instance which represents an establish two-way communication channel to the device chosen (and holds resources, like sockets). The `MessageListener` passed to `connect(..)` call will receive all the `Message`s coming _from_ the device. `Conversation` will try it's best to recover from underlying transport failures. A `Connection` should be closed via `close()` call when no more communication is to be carried out.
5. `Connector#connect(DiscoveryResultItem, String, MessageListener)` will block and should be called outside of main thread.
6. Caller can pass optional `executor` argument to `connect` call to determine executor that will execute `send` callbacks.

## Payloads

Particular payloads that can be sent over the `Conversation` are specified elsewhere.
For convenience reasons SDK provides `PayloadFactory` to generate some common payloads. See `Connector#getPayloadFactory()`.

## Security

`Connector.connect` and `Connector.discover` require current user's OAuth token in `Yandex.Passport` to access quasar backend for security reasons.
The token must have a scope of `quasar:all`. NB: the scope will be different.

## Device connection/conversation

1. Connection to a device is represent basically by `Conversation` class. Its' heir `LiveConnection` marks that actual websocket-connections can switch within a `LiveConnection`-object.
2. A `Conversation` instance enables sending commands to the device and receving status and callback messages from it. There are two main methods of sending a command:
   * `Conversation.send(Payload)` to fire-and-forget some message.
   * `Converstaion.send(Payload, ResponseListener)` to send a message and notify a listener when device answers on that call. Listener may be never notified if a communication problem occurs, no retries are made on the behalf of the SDK
3. A `ReponseListener` passed to the `Conversation.send(Payload, ResponseListener)` get a `ResponseMessage` object when notified of a `send(..)` result. This object allows caller to find out the command's outcome via `ResponseMessage#getStatus()` method, which returns:
   * `ResponseMessage.Status.SUCCESS` when command was understood and carried-out successfully
   * `ResponseMessage.Status.FAILURE` when command was unserstood but a problem occured during it's execution (e.g. the music to be played was not found on the back-end)
   * `ResponseMessage.Status.UNSUPPORTED` when command was not understood (e.g. when new command was sent to a device with old firmware)
4. To create a proper `Payload` use a `PayloadFactory` instance, normally acquired via `Connector.getPayloadFactory()`. `PayloadFactory` provides convenience methods like `getPlayMusicPayload(String, String)` or `getSetVolumePayload(Double)`.
5. One special payload provided is one created via `PayloadFactory#getStatusSubscribePayload(Double)`. When processed, it causes device to start sending periodic status messages over current `Conversation`.

## Notes
1. Current `Discovery` implementation acquires `WifiManager.MulticastLock` while not yet closed. As per it's documentation, it may cause extra load on system. User SHOULD `close()` the `Discovery` when done to prevent battery drain.

## Installing

Add repo and dependency to your `build.gradle`:
```gradle
repositories {
    maven { url "https://artifactory.yandex.net/yandex_quasar_releases/" }
}

...

dependencies {
    ...
    implementation 'ru.yandex.quasar:glagol:3.0.0.0-SNAPSHOT'
}
```

## Developing and publishing

To publish new version, set version value into `gsdk` var in versions.gradle 

```
./gradlew :android:clean :android:build :android:publish
```

### Troubleshooting
If you are facing with certificate issues during publish like:
```
sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
```
then check how to fix it here: https://wiki.yandex-team.ru/security/ssl/sslclientfix/