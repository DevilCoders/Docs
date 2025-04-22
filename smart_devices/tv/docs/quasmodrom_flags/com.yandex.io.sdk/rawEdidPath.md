# rawEdidPath
**Type:** String
**Default:** ""

**Related tickets**
[TVANDROID-5396](https://st.yandex-team.ru/TVANDROID-5396)

**Context**
```json
{
    "com.yandex.io.sdk": {
        "rawEdidPath": "value"
    }
}
```

**Description**
Description for default configs stored in `tv/services/sdk-iosdk/src/main/assets`. Configs are
device-specific, meaning that we use different files for different devices (e.g. tv, module, etc.)

path to the EDID file

