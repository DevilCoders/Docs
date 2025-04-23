# serviceEnabled
**Type:** nan
**Default:** nan

**Related tickets**
[TVANDROID-5613](https://st.yandex-team.ru/TVANDROID-5613)

**Context**
```json
{
  "com.yandex.tv.services": {
    "accessibilityConfig": {
      "serviceEnabled": false,
      "notificationTimeoutMs": 100,
      "packages": [
        "com.yandex.tv.home",
        "com.yandex.tv.services",
        "stub"
      ]
    }
  }
}
```

**Description**


Включает YandexAccessibilityService и конфигурирует параметры из [https://developer.android.com/reference/android/accessibilityservice/AccessibilityServiceInfo#xml-attributes_1](https://developer.android.com/reference/android/accessibilityservice/AccessibilityServiceInfo#xml-attributes_1)

