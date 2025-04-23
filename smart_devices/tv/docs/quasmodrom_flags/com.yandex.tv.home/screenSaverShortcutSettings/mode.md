# mode
**Type:** Bool String[singleTap, doubleTap, longPress] Long Long
**Default:** %%(json) "com.yandex.tv.home": {  "screenSaverShortcutSettings": {    "enabled": false,    "mode": "doubleTap",    "doubleTapInterval": 500,    "longPressInterval": 2000   } } %%

**Related tickets**
[TVANDROID-5920](https://st.yandex-team.ru/TVANDROID-5920)

**Context**
```json
{
  "com.yandex.tv.home": {
    "screenSaverShortcutSettings": {
      "enabled": true,
      "mode": "singleTap",
      "doubleTapInterval": 500,
      "longPressInterval": 2000
    }
  }
}
```

**Description**

Конфигурация шортката для включения скринсейвера
