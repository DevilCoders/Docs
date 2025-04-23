# compatibleRemoteControllers
**Type:** Array\<String\>
**Default:** []

**Related tickets**
[TVANDROID-5396](https://st.yandex-team.ru/TVANDROID-5396)

**Context**
```json
{
    "com.yandex.tv.setupwizard": {
        "compatibleRemoteControllers": [
            "names"
        ]
    }
}
```

**Description**
Description for default configs stored in `tv/services/sdk-iosdk/src/main/assets`. Configs are
device-specific, meaning that we use different files for different devices (e.g. tv, module, etc.)

names of supported remote controllers to check them when establishing a bluetooth connection.
