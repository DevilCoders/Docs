# dnsFallbackEnabled
**Type:** Bool, Array
**Default:** false ["yandex.ru", "yandex.net"]

**Related tickets**
[TVANDROID-5910](https://st.yandex-team.ru/TVANDROID-5910)

**Context**
```json
{
  "yandexTvGeneral": {
    "dnsFallbackEnabled": false,
    "dnsFallbackWhitelist": [
      "yandex.ru",
      "yandex.net"
    ]
  }
}
```

**Description**
 включает использование [https://wiki.yandex-team.ru/users/viktor-reznik/podderzhka-yandex-dns-v-kachestve-follbeka-sistemnomu-dns-v-okhttp/](https://wiki.yandex-team.ru/users/viktor-reznik/podderzhka-yandex-dns-v-kachestve-follbeka-sistemnomu-dns-v-okhttp/)
 в апдейтере для походов во все ручки. Может быть использовано и в других местах, код встроен в common:network
dnsFallbackWhitelist: необязательный, эффективен только с `dnsFallbackEnabled`
Список хостов, для использования YandexDns, если основной их не зарезолвил
