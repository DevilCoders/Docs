# repeatEnabled
**Type:** Bool Int[0, 100] Bool 
**Default:** false 0 false

**Related tickets**
[TVANDROID-5334](https://st.yandex-team.ru/TVANDROID-5334)

**Context**
```json
{
  "com.yandex.tv.home": {
    "detailsScreenVideoPreviewV2": {
      "enabled": true,
      "volume": 0,
      "repeatEnabled": true
    }
  }
}
```

**Description**
 настройки фонового трейлера в карточке деталей
`enabled` - включение/отключение трейлера
`volume` - громкость видео (0 - без звука, 100 - максимальная громкость)
`repeatEnabled` - включение зацикливания трейлера, при отключении, после завершения трейлер меняется на обложку
