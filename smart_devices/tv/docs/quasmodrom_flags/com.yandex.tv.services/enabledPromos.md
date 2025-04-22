# enabledPromos
**Type:** Array of Strings
**Default:** %%(json) [] %%

**Related tickets**
[TVANDROID-5179](https://st.yandex-team.ru/TVANDROID-5179)
[TVANDROID-5194](https://st.yandex-team.ru/TVANDROID-5194)

**Context**
```json
{
  "com.yandex.tv.services": {
    "enabledPromos": [
      "promo1",
      "promo2"
    ]
  }
}
```

**Description**
Включенные промо, для которых будет произведена попытка сходить (на бекенд) за дивной версткой, чтобы отрисовать.



В данный момент доступно 1 промо `"gift_on_main"` из 
