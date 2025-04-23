# Работа с переводами

- Переводы лежат в [Танкере](https://tanker.yandex-team.ru/project/yandex_lavka?branch=bunker).

- Ветка: `bunker`

- Для работы с переводами на уровне кода используется утилита [i18n](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/i18n?rev=r8039043)

- Для создания ключей в Танкере и выгрузки переводов, используется [tanker-kit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit?rev=r8039043)

- Оригинальный язык - Русский
- Языки для переводов - Английский, Французский, Иврит

## Структура

На уровне проекта существуют кейсеты. Кейсет содержит ключи. Ключ имеет переводы на нужные языки.

## Работа с танкером

Танкер использует `OAuth-токен` для авторизации к своему API. Для генерации персонального токена перейдите по ссылке https://nda.ya.ru/3SjQY7. Затем экспортируйте ключ в ваш `$HOME/.profile` (или `.bash_profile`, если не сработало), добавив

```bash
export TANKER_API_TOKEN="Тут ваш OAuth токен для Танкера"
```

## Использование

```ts
import { i18n } from 'i18n'

// i18n - объект, в котором имена ключей являются именами кейсетов
// Значения объекта - функции, в которые передается имя ключа и опциональные параметры
i18n.common('key')
```

### Параметризация

Параметры в ключах объявляются в синтаксисе схожем с параметрами для template strings.

```ts
// i18n/cache.json
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

### Плюрализация

```ts
// i18n/cache.json
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

### Интеграция с компонентами

```ts
// i18n/cache.json
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

## Как добавить новые ключи

**ВАЖНО**
При выгрузке в `cache.json`, берутся только используемые в коде ключи.
Поэтому необходимо их использовать явно

- Ключ попадет в `cache.json`

```ts
i18n.keyset('key')
```

- Ключ НЕ попадет в `cache.json`

```ts
const KEY_ID = 'key'
i18n.keyset(KEY_ID)
```

### Создаем ключи вручную

1. Идем в [проект в Танкере](https://tanker.yandex-team.ru/project/yandex_lavka?branch=bunker)

2. Если для ключа нужен новый кейсет, создаем кейсет.

3. Переходим в соответствующий кейсет и жмем в правом верхнем углу `Добавить ключи`.
   Указываем их названия, русские переводы - жмем `Создать ключи` внизу

4. Когда переводы будут готовы, подтягиваем их из танкера

```bash
npx tanker pull
```

5. Используем в коде

```ts
i18n.keyset('key')
```

## <a name="Form"></a> Как заказать переводы на другие языки

1. Идем в [дневной тикет](<https://st.yandex-team.ru/TAXILOC/order:updated:false/filter?resolution=empty()&type=2&status=open&tags=taxi_daily>) очереди [TAXILOC](https://st.yandex-team.ru/TAXILOC/)

2. Пишем в комментарии ключи, которые нужно перевести, и языки

```
https://tanker.yandex-team.ru/project/yandex_lavka/keyset/a11y/key/app-store-download%40%40desktop?branch=bunker
https://tanker.yandex-team.ru/project/yandex_lavka/keyset/a11y/key/card-binding-title%40%40desktop?branch=bunker
Нужны en, fr, he
```

## Типизация

Типы генерируются при исполнении следующей команды:
```bash
npm run types:i18n
```

И прописываются в `i18n/types`
