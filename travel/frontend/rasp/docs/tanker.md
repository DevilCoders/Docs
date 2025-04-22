# Базовая инфа

-   Текущая ссылка на основную ветку танкера: https://tanker.yandex-team.ru/project/rasp-morda-front?branch=master
-   Информация о функционале Tanker: https://wiki.yandex-team.ru/portal/international/tanker/api/v2/
-   При импорте в билд попадает языковая версия заданная через переменную окружения `BUNDLE_LANGUAGE`

## Синхронизация проекта с танкером

Для загрузки кейсета переводы в нем должны быть подтверждены (кнопка подтвердить все переводы).

Актуализировать конкретный кейсет в проекте: `npm run i18n.get -- --name=nameKeyset`
Актуализировать все кейсеты в проекте: `npm run i18n.get -- --updateExists`

## Использование переменных

Формат в танкере:

```
С {{start}} по {{end}}
```

Использование в коде:

```
import timeKeyset from '../../i18n/time';

const title = timeKeyset('interval', {
  start: '12 апреля',
  end: '19 мая'
});
```

-   Использование i18n переменных:

Формат в танкере:

```
Ещё {{someCount}} {{plural count=count one="направление" some="направления" many="направлений" }}
```

Использование в коде:

```
import keyset from '../../i18n/someKeyset';

const title = keyset('omgkey', {
  someCount: 15,
  count: 205
});
```
