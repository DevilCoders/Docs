Mail 360 In app purchases library for android

Usage by sources:
In build.gradle:
```
    include ':mail360-purchase'
    project(':mail360-purchase').projectDir = file("<relative-path-to mobile/common>/android/mail360-purchase/")
```

settings.gradle:
```
apply from: "<relative-path-to mobile/disk/common>/gradle/settings.gradle"
    includeCommonDiskModules(
            '<relative-path-to mobile/disk/common>/modules/',
            'logger', 'concurrency', 'http-client', 'datetime', 'api', 'iap', 'spaceutils'
    )
```

In Application.onCreate() initialize library:
```
InApp360Components.initialize(config)
```

To use library access to library features create instance of PurchaseComponentsProvider for user's uid:
```
InApp360Components.createProvider(uid, userConfig)
```
if uid = null then library will works in anonymous mode (all features will be disabled)

Sync tanker:
```
./sync_tanker.sh
```
