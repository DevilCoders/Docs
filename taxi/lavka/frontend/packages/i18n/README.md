## Table of Contents
1. [Работа с переводами](#translate-work)
   1. [Структура](#structure)
   2. [Работа с танкером](#work-with-tanker)
   3. [Использование](#usage)
      1. [Параметризация](#parametrization)
      2. [Плюрализация](#pluralization)
      3. [Интеграция с компонентами](#components-integration)
   4. [Как добавить новые ключи](#how-to-add-new-keys)
   5. [Как заказать переводы на другие языки](#how-to-order)
   6. [Типизация](#typings)


# Работа с переводами <a name="translate-work"></a>

- Переводы лежат в [Танкере](https://tanker.yandex-team.ru/project/yandex_lavka?branch=bunker).

- Ветка: `bunker`

- Для работы с переводами на уровне кода используется утилита [i18n](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/i18n?rev=r8039043)

- Для создания ключей в Танкере и выгрузки переводов, используется [tanker-kit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit?rev=r8039043)

- Оригинальный язык - Русский
- Языки для переводов - Русский, Английский, Иврит

## Структура <a name="structure"></a>

На уровне проекта существуют кейсеты. Кейсет содержит ключи. Ключ имеет переводы на нужные языки.

## Работа с танкером <a name="work-with-tanker"></a>

Танкер использует `OAuth-токен` для авторизации к своему API.

При первом запуске проекта будет предложено ввести этот токен

![example](https://jing.yandex-team.ru/files/rifler/2022-07-04_17-23-33.png "example")


Если что-то пойдёт не так, то эти действия можно провернуть вручную:
1. перейти по ссылке https://nda.ya.ru/3SjQY7
2. Создать файл `.env` в корне пакета и написать в него `TANKER_TOKEN={your token here}`


## Использование <a name="usage"></a>

```ts
import { i18n } from 'i18n'

// i18n - объект, в котором имена ключей являются именами кейсетов
// Значения объекта - функции, в которые передается имя ключа и опциональные параметры
i18n.common('key')
```

### Параметризация <a name="parametrization"></a>

Параметры в ключах объявляются в синтаксисе схожем с параметрами для template strings.

```ts
// src/cache.json
{
  "en": {
    "common": {
      "metroName": {
        "isPlural": false,
        "form": "subway {metro}"
      }
    }
  }
  ...
}
```

```ts
i18n.common('metroName', { metro: 'Парк Культуры' })
```

### Плюрализация <a name="pluralization"></a>

```ts
// src/cache.json
{
  "ru": {
    "common": {
      "remainingMinutes": {
        "isPlural": true,
        "one": "Осталась {count} минута",
        "some": "Осталось {count} минуты",
        "many": "Осталось {count} минут",
        "none": "Время закончилось"
      }
    }
  }
  ...
}
```

```ts
i18n.common('remainingMinutes', { count: 5 })
```

### Интеграция с компонентами <a name="components-integration"></a>

```ts
// src/cache.json
{
  "ru": {
    "common": {
      "linkKey": {
        "isPlural": false,
        "form": "OOO «{link}»"
      }
    }
  }
  ...
}
```

```ts
import { i18n, i18nRaw } from 'i18n'

i18nRaw.common('linkKey', {
  link: (
    <Link url="#" key="key">
      {i18n.common('world')}
    </Link>
  ),
})
```

## Как добавить новые ключи <a name="how-to-add-new-keys"></a>

1. Идем в [проект в Танкере](https://tanker.yandex-team.ru/project/yandex_lavka?branch=bunker)

2. Если для ключа нужен новый кейсет, создаем кейсет.

3. Переходим в соответствующий кейсет и жмем в правом верхнем углу `Добавить ключи`.
   Указываем их названия, русские переводы - жмем `Создать ключи` внизу

4. Когда переводы будут готовы, подтягиваем их из танкера

```bash
npm run i18n:pull
```

5. Используем в коде

```ts
i18n.keyset('key')
```

## <a name="Form"></a> Как заказать переводы на другие языки <a name="how-to-order"></a>

1. Идем в [дневной тикет](<https://st.yandex-team.ru/TAXILOC/order:updated:false/filter?resolution=empty()&type=2&status=open&tags=taxi_daily>) очереди [TAXILOC](https://st.yandex-team.ru/TAXILOC/)

2. Пишем в комментарии ключи, которые нужно перевести, и языки

```
https://tanker.yandex-team.ru/project/yandex_lavka/keyset/a11y/key/app-store-download%40%40desktop?branch=bunker
https://tanker.yandex-team.ru/project/yandex_lavka/keyset/a11y/key/card-binding-title%40%40desktop?branch=bunker
Нужны en, fr, he
```

## Типизация <a name="typings"></a>

Типы генерируются при подтягивании переводов при исполнении следующей команды:
```bash
npm run i18n:pull
```
