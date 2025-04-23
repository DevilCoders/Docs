# searchAppUrl
**Type:** String
**Default:** %%"https://yandex.ru/quasar/external/open-module-group-settings?moduleId=DEVICE_ID&modulePlatform=PLATFORM"%%

**Related tickets**
[TVANDROID-4938](https://st.yandex-team.ru/TVANDROID-4938)

**Context**
```json
{
  "com.yandex.tv.services": {
    "tandemSetup": {
      "searchAppUrl": "value"
    }
  },
  "com.yandex.tv.setupwizard": {
    "tandemSetup": {
      "searchAppUrl": "value"
    }
  }
}
```

**Description**
Заменяет урл, который зашифрован в QR-код на экране создания тандема в суве.
 
