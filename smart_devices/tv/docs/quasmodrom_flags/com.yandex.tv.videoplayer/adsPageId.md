# adsPageId
**Type:** String
**Default:** -

**Related tickets**
[TVANDROID-3560](https://st.yandex-team.ru/TVANDROID-3560)

**Context**
```json
{
  "com.yandex.tv.videoplayer": {
    "adsPageId": "value"
  }
}
```

**Description**
Задание рекламного pageId для отладки. В бою - pageId привязан к каждому конкретному видео. Вручную размечают в ВХ.
`1378525` - реклама с adPod-ами, приходит не гарантированно
`R-M-DEMO-instream-vmap` - реклама без adPod-ов, зато приходит гарантированно


