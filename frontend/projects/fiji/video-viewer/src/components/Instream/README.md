## Сценарии instream рекламы
Задача с деталями: [VIDEOUI-13289](https://st.yandex-team.ru/VIDEOUI-13289)

Флаги:
- ``video_instream_vh_desktop_config`` - десктопы
- ``video_instream_vh_touch_config`` - тачи

Пример формата флага:
``20_21:621485-2,51:621485-1``

Здесь:
   - `20_21` - это 20 и 21 категория видео (`content_type_id`)
   - `621485` - номер площадки (параметр `partner_id`)
   - `2` - номер сценария (параметр `vmap_id`)

Прокидывание параметров в vh-плеер осуществляется через url вида:
`https://frontend.vh.yandex.ru/player/17466075843501816389?sandbox_version=0x2b2c1f89197&partner_id=621485&vmap_id=1`

Дополнительная информация по сценариям:
- [Информация по монетизации Видеохостинга](https://wiki.yandex-team.ru/users/oxapolyak/Monetizacija-Videoxostinga/#nastrojjki)
