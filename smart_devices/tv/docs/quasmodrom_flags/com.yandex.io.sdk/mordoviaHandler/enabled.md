# enabled
**Type:** Object
**Default:** {}

**Related tickets**
None

**Context**
```json
{
  "com.yandex.io.sdk": {
    "mordoviaHandler": {
      "enabled": false
    }
  }
}
```

**Description**
Настройки для iosdk-app
`mordoviaHandler.enabled == false` выключает трансформацию для мордовийных комманд `mordovia_show` и `mordovia_command` в `go_home`
