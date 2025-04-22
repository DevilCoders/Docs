# rootFallbackCerts
**Type:** Bool, Array\<String\>
**Default:** false, []

**Related tickets**
[TVANDROID-5910](https://st.yandex-team.ru/TVANDROID-5910)

**Context**
```json
{
  "yandexTvGeneral": {
    "certificatesFallbackEnabled": false,
    "rootFallbackCerts": [
      "stub"
    ]
  }
}
```

**Description**

Включает доверие дополнительным рутовым сертификатам. По дефолту - серту минцифры.
rootFallbackCerts: необязательный, эффективен только с certificatesFallbackEnable=true.
Содержит Base64-encoded сертификаты, которым доверяем в апдейтере (возможно использование и в других приложениях).
