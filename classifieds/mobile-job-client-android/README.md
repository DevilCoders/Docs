[master: ![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Rabota_MobileRabotaClientAndroid_Master/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Rabota_MobileRabotaClientAndroid_Master)

[dev: ![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Rabota_MobileJobClientAndroid_DemoTest/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Rabota_MobileJobClientAndroid_DemoTest)


Yandex libraries android sample
===================
See more at https://st.yandex-team.ru/ANDROIDLIB-57

Teamcity: http://teamcity.mobile.dev.yandex.net/viewType.html?buildTypeId=MobileAndroidSample_MasterWithWatchedRefs 

Github: https://github.yandex-team.ru/thevery/YandexAndroidSample

Stash: TBD 

Supported features
===================
 - gradle 2.1 with wrapper
 - gradle android plugin 0.13.0
 - java 7
 - versionCode teamcity integration
 - dev/production flavors with configurable metrica keys, logs and some other params (see MyActivity#setHostInfo) 

Supported libraries
===================
 - Metrica (mobmetricalib-internal:1.50) with explicit manifest 
 - Upload beta (gradle-upload-beta-plugin:1.4-SNAPSHOT)
 
Gradle notes
===================
 - proguard disabled by using 'do nothing' rules (see `proguard-disabled.pro`)
 - Integer.MAX_VALUE is used as versionCode for local build to install local build over server build
 - java 7 enabled by `compileOptions` options (see supported features at http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Using-sourceCompatibility-1.7)
 - `buildConfigField` gets compiled to `BuildConfig` class constants
 - use predefined ${applicationId} placeholder instead of package name for external libraries like metrica and OpenPush in final application manifest
 - use custom ${realApplicationId} placeholder instead of predefined ${applicationId} to force placeholder resolution at app build time (not library build time) in module manifest
 - use `rootProject.ext` to change values for all modules in one place

Teamcity notes
===================
General settings
 - Build number format: do not change
 - Build counter: will be converted to BuildConfig.VERSION_CODE read via getBuildNumber() in build.gradle
 - Artifact paths: 
 - Build Steps: use auto-detect or add Gradle manually
 - Gradle: use wrapper,  

Repository settings
 - Separate fetch and push (for taker) URLs
 - Root name: git://github.yandex-team.ru/thevery/YandexAndroidSample.git becomes thevery/YandexAndroidSample
 - Default branch: refs/heads/ is optional
 - Branch specification: `+:refs/heads/*` to watch all branches, `+:refs/pull/(*/merge)` to watch for pull requests, `()` to print full name
 - Username style: Author Name and Email
 - Authentication method: default private key with empty username
