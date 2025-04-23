# mandatoryAuth
**Type:** Bool
**Default:** false

**Related tickets**
[TVANDROID-5396](https://st.yandex-team.ru/TVANDROID-5396)

**Context**
```json
{
    "yandexTvGeneral": {
        "mandatoryAuth": "true/false"
    }
}
```

**Description**
Description for default configs stored in `tv/services/sdk-iosdk/src/main/assets`. Configs are
device-specific, meaning that we use different files for different devices (e.g. tv, module, etc.)

whether authorization is mandatory for this device. If it is, most of functionality must be hidden until user is authorized.
