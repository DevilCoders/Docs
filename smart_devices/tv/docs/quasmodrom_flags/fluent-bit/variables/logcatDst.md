# logcatDst
**Type:** logcatDst:String, libLogsDst:String, logcatLogBufferSize:String
**Default:** logcatDst: отсутствует, libLogsDst: "http", logcatLogBufferSize: "1048576"

**Related tickets**
[TVANDROID-5421](https://st.yandex-team.ru/TVANDROID-5421)

**Context**
```json
{
  "fluent-bit": {
    "variables": {
      "logcatDst": "http",
      "libLogsDst": "http",
      "logcatLogBufferSize": "1048576"
    }
  }
}
```

**Description**
      `logcatDst`: "http" - включает отправку логов logcat, любое другое значение - выключает. 
      `libLogsDst`: управляет старым способом отправки логов демонов. "http" - включает, любое другое значение выключает. 
      `logcatLogBufferSize`: размер буфера логирования в байтах. 


