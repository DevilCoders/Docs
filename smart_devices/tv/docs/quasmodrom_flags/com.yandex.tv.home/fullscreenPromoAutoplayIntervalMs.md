# fullscreenPromoAutoplayIntervalMs
**Type:** Bool Int
**Default:** false 12000

**Related tickets**
[TVANDROID-5697](https://st.yandex-team.ru/TVANDROID-5697)

**Context**
```json
{
  "com.yandex.tv.home": {
    "fullscreenPromo": "true/false",
    "fullscreenPromoAutoplayIntervalMs": "ms"
  }
}
```

**Description**

`fullscreenPromo` включает фулскрин-промоблок на домашнем экране
` fullscreenPromoAutoplayIntervalMs` время автоперелистывания элементов промоблока в мс. Автоперелистывание включено, если ` fullscreenPromoAutoplayIntervalMs > 0`
