# Vertical services - Android core libraries

[master: ![Build Status](https://teamcity.mobile.dev.yandex.net/app/rest/builds/buildType:VerticalMobile_Library_Android_MobileVerticalLibsAndroid_Master/statusIcon)](https://teamcity.mobile.dev.yandex.net/viewType.html?buildTypeId=VerticalMobile_Library_Android_MobileVerticalLibsAndroid_Master)

[dev: ![Build Status](https://teamcity.mobile.dev.yandex.net/app/rest/builds/buildType:VerticalMobile_Library_Android_MobileVerticalLibsAndroid_Dev/statusIcon)](https://teamcity.mobile.dev.yandex.net/viewType.html?buildTypeId=VerticalMobile_Library_Android_MobileVerticalLibsAndroid_Dev)

[some kind of changelog](CHANGELOG.md)

[Some documentation](https://wiki.yandex-team.ru/vsapps/Vertical-Core-Android/)

[**Tasks TODO**](https://st.yandex-team.ru/VSAPPS/order:updated:false/filter?resolution=empty()&components=28132)

## Integration

```
repositories {
    maven { url 'http://artifactory.yandex.net/artifactory/public/' }
}

def verticalLibsVersion = '0.21.2'
//when you have made changes in libraries and want to test them in your app, before pushing
def verticalLibsDevMode = verticalLibsVersion.endsWith("SNAPSHOT")

if (verticalLibsDevMode) {
    //refresh vertical libs on each gradle sync
    configurations.all {
        resolutionStrategy.cacheChangingModulesFor 0, 'seconds'
    }
    repositories {
        maven {name "local"; url "file://${System.getProperty('user.home')}/.yandex-mobdev/m2/"}
    }
}

dependencies {
    compile ("com.yandex.android.vertical:vertical-core:$verticalLibsVersion") {
        changing = verticalLibsDevMode
    }
}
```

# WARNING
In version 0.3.x AM helpers was move to separate library - vertical.auth. If you need AM usage in your app,
please, read migration section carefully.

## Migration from version 0.2.x to 0.3.0 :

- In your Base*Activity you should call AmHelper.onActivityResult.

## Migration from 0.5.* to 0.6.0

1. [AM migration](https://wiki.yandex-team.ru/yandexmobile/accountmanager/help/android/migration/#r310tor400)
2. KeyHolder.METRICA_API_KEY() is not needed for AM.
