# Yandex Advertisement Identifier Service

Yet another advertisement identifier provider. The main purpose is to provide unique resettable device-wide identifier for devices without any other provider (Google Advid, Huawei Oaid and etc.).

## Retrieving identifier information

Usually you do not need to retrieve this identifier from Yandex Advid Service. If you are using **AppMetrica** it will make all the job for you. And you can get all identifiers that AppMetrica collected.
But if you still want to interact with Advid Service directly (or you are adding this identifier support into AppMetrica), you need to follow these steps:

1. Add *client* *.aidl files folder to your source root
    
   ```gradle
   android {
        sourceSets {
            main.aidl.srcDirs += ['${pathToYandexAdvidProjectDirectory}/common/client/aidl']
        }
   }
   ```
2. Add `<query>` to you manifest
   
   ```
   <queries>
        <intent>
            <action android:name="com.yandex.android.advid.IDENTIFIER_SERVICE" />
        </intent>
    </queries>
   ```
   
3. Bind to **AdvidService** by action using explicit intent (intent with package).

    ```kotlin
    context.bindService(
        Intent("com.yandex.android.advid.IDENTIFIER_SERVICE").setPackage("com.yandex.android.advid"),
        connection, Context.BIND_AUTO_CREATE
    )
    ```

4. Obtain *YandexAdvIdInterface* from Binder in your *onServiceConnected*
    
    ```kotlin
    advIdService = YandexAdvIdInterface.Stub.asInterface(service) 
    ```
   
5. Use *YandexAdvIdInterface* to retrieve identifier and *trackingLimited* flag.

For full integration example see [SettingsActivity](./sample/src/main/java/com/yandex/android/advid/sample/SettingsActivity.kt) in the sample project.

## Integration into the firmware 

There can be only one identifier service of each kind in the system.
Yandex Advid Service is a standalone application shipped as an integral part of the OS (shell). And it must be protected from uninstalling. Service application does not provide any UI for identifier management. Thus, firmware developer must support *Advid Service Management* screen by itself. The best place for it is somewhere in the **Settings** application.
Yandex Advid Service can be managed via *AIDL* interface. It provides the ability to retrieve or generate new advid and to limit identifier tracking. 
Controlling service is protected by the permission:
```xml
    <permission android:name="com.yandex.android.permission.ADVID_MANAGEMENT"
        android:protectionLevel="signature|privileged"/>
```
As *Yandex Advid Service* app is signed with the default Yandex release key, it can be accessed from any other Yandex application or system application (like *Settings*). 

To add the ability to manage Yandex Advid to your application you need to follow these steps:

1. Add *controller* *.aidl files folder to your source root
    
   ```gradle
   android {
        sourceSets {
            main.aidl.srcDirs += ['${pathToYandexAdvidProjectDirectory}/common/controller/aidl']
        }
   }
   ```

2. Add `<query>` to you manifest
   
   ```
   <queries>
        <intent>
            <action android:name="com.yandex.android.advid.MANAGE_IDENTIFIERS" />
        </intent>
    </queries>
   ```
   
3. Request permission in your manifest file

    ```xml
    <uses-permission android:name="com.yandex.android.permission.ADVID_MANAGEMENT"/>
    ```
   
4. Bind to **AdvidControllerService** by action using explicit intent (intent with package).
   
   ```kotlin
   context.bindService(
       Intent("com.yandex.android.advid.MANAGE_IDENTIFIERS").setPackage("com.yandex.android.advid"),
       connection, Context.BIND_AUTO_CREATE
   )
   ```
   
5. Obtain *YandexAdvIdController* from Binder in your *onServiceConnected*
    
    ```kotlin
    advIdController = YandexAdvIdController.Stub.asInterface(service) 
    ```

For full integration example see [ControllerActivity](./sample/src/main/java/com/yandex/android/advid/sample/ControllerActivity.kt) in the sample project.
