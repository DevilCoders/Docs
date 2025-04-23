# Профиль вождения

## Конфигурирование

Для конфигурирования профиля вождения (v2) используются как GVars, так и локализации. Вместо GVars допустимо использование экшенов `override_settings`, однако это крайне не рекомендуется в силу возможного возникновения проблем конфигурации в отдельных случаях.

В профиле вождения выделяются этапы, такие как:

* Блокировка.
* Испытательный срок.
* Повышенные цены.
* Обычный статус (Все хорошо, Супер-молодец).

Каждый этап имеет свой уникальный идентификатор. Для блокировки это будет название тега, если для него указана конкретная конфигурация в профиле вождения, либо `block_stage` &mdash; для всех остальных блокировок. У испытательного срока идентификатор `trial_stage`, у повышенной цены `price_up_stage`. У обычных статусов идентификаторы имеют следующий вид: `stage_1`, `stage_2`, ...

Зная идентификатор можно сконфигурировать локализацию для профиля вождения:

`driving_profile.stage.ID.units`
`driving_profile.stage.ID.caption`
`driving_profile.stage.ID.sub_caption`
`driving_profile.stage.ID.descriptions_title`

В локализациях для этапов блокировки доступны следующие макросы:

`_BlockDays_` &mdash; количество дней проведенных в блокировке.
`_BlockTotalDays_` &mdash; общая длительность блокировки.
`_BlockRemainedDays_` &mdash; количество оставшихся дней.
`_BlockEndDate_` &mdash; дата завершения блокировки.

Описание одного этапа имеет следующую схему:

```(json)
{
  "prev_color": "#B44B00",
  "next_color": "#E38800",
  "description_ids": [
    "description_1",
    "description_2",
    "description_3"
  ],
  "from_value": 0.07,
  "begin_value": 0.069,
  "end_value": 0.25,
  "begin_points": 10,
  "end_points": 39
}
```

Чтобы описать этап блокировки нужно использовать GVars `driving_profile.block_stage` либо `driving_profile.block_stage.TAG_NAME`.

Чтобы описать этап испытательного срока нужно использовать GVars `driving_profile.trial_stage`.

Чтобы описать этап повышения цены нужно использовать GVars `driving_profile.price_up_stage`.

Для обычных этапов нужно использовать GVars `driving_profile.stages` со следующей схемой:

```(json)
{
  "stages": [
    {
      "from_value": 0.01,
      "begin_value": 0.01,
      "end_value": 0.07,
      "next_color": "#8C32FF",
      "prev_color": "#BF57F0",
      "description_ids": [
        "description_1",
        "description_2",
        "description_3"
      ],
      "begin_points": 40,
      "end_points": 80
    },
    {
      "from_value": 0,
      "begin_value": 0,
      "end_value": 0.01,
      "next_color": "#F8B301",
      "prev_color": "#a8d102",
      "description_ids": [
        "description_1",
        "description_2",
        "description_3"
      ],
      "begin_points": 81,
      "end_points": 100
    }
  ]
}
```

В каждом этапе перечисляется список идентификаторов описаний. Для описаний используется локализация:

`driving_profile.stage_description.ID.text`

А также GVars:

`driving_profile.stage_description.ID.icon`

{% cut "Старый профиль вождения (v1)" %}

Конфигурирование профиля вождения в основном осуществляется через использование GVars:

* `aggression.value_epsilon` (действительное число) &mdash; минимальный порог для изменения последнего значения скоринга (для "стало лучше/хуже").
* `aggression.user_tag` (строка) &mdash; название тега хранящего текущее значение скоринга пользователя.
* `aggression.trial_tag` (строка) &mdash; название тега хранящего текущее значение пробега для пробного периода.
* `aggression.block_tags` (строка) &mdash;  список тегов (через запятую "`,`") блокировки за агрессию.
* `aggression.price_up_tag` (строка) &mdash; название тега хранящего признак повышения цены.

{% endcut %}

### Повышенный кешбек

Для повышенного кешбека следует использовать следующие GVars:

* `aggression.notification.high_cashback.roles` &mdash; название ролей с повышенным кешбеком (через запятую "`,`").
* `aggression.notification.high_cashback` &mdash; описание блока кешбека.
* `aggression.notification.high_cashback.no_plus` &mdash; описание блока кешбека (без плюса).

### Достижения (или Ачивки)

Каждая ачивка представляет из себя тег со следующими важными полями:

`level` &mdash; уровень ачивки (количество полученных ачивок).
`level_value` &mdash; прогресс ачивки.

#### Локализация
`achievement_user_tag.TAG.full_subtitle`
`achievement_user_tag.TAG.no_level_progress_title`
`achievement_user_tag.TAG.no_progress_sub_title`
`achievement_user_tag.TAG.progress_title`
`achievement_user_tag.TAG.sub_title`
`achievement_user_tag.TAG.title`

`achievement_user_tag.TAG.LEVEL.full_subtitle`
`achievement_user_tag.TAG.LEVEL.no_progress_sub_title`
`achievement_user_tag.TAG.LEVEL.progress_title`
`achievement_user_tag.TAG.LEVEL.sub_title`
`achievement_user_tag.TAG.LEVEL.title`
где `TAG` и `LEVEL` &mdash; название тега и уровень соответсвенно. Пустой уровен = `0`.


В локализациях доступны следующие макросы:

`_LevelValue_` &mdash; текущее значение на текущем уровне ачивки.
`_MaxLevelValue_` &mdash; максимальное значение для получения следующего уровня.
`_RemainedLevelValue_` &mdash; оставшееся значения для получения следующего уровня.
