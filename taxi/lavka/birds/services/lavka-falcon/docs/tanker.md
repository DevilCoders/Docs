# Танкер

[Проект в Танкере](https://tanker.yandex-team.ru/project/lavka-falcon)

Танкер использует `OAuth-токен` для авторизации к своему API. Для генерации персонального токена перейдите по ссылке https://nda.ya.ru/3SjQY7. Затем экспортируйте ключ в ваш `$HOME/.profile` (или `.bash_profile`, если не сработало), добавив:

```bash
export TANKER_API_TOKEN="Тут ваш OAuth токен для Танкера"
```

Для синхронизации переводов используется [tanker-kit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md).

`.tanker` - это служебный каталог, в котором хранятся конфигурационный файл для `tanker-kit`, парсер, диспатчер.

## Использование

> `i18n(keyset, key [, options]);`

> `i18nRaw(keyset, key [, options]);`

Перевод хранится в `key`, а `key` хранится в `keyset`:

```json
{
    "my-keyset": {
        "my-key": "Метро Парк Культуры находится в той стороне"
    }
}
```

Файлы с переводами для конкретного языка хранятся в папке `./src/i18n/translations/...`.

Затем мы используем эти переводы внутри компонентов через hook `useI18n` или `useI18nRaw`:

```ts
import {useI18n} from '@/src/i18n';

const i18n = useI18n();

i18n('my-keyset', 'my-key');
```

### Параметры

Параметры объявляются в синтаксисе схожем с параметрами для template strings:

```json
{
    "my-keyset": {
        "my-key": "Метро {metro} находится в той стороне"
    }
}
```

и передаются третим аргументом в функцию:

```ts
import {useI18n} from '@/src/i18n';

const i18n = useI18n();

i18n('my-keyset', 'my-key', {metro: 'Парк Культуры'});
```

### Плюрализация

Для определённого колличества свой перевод:

```json
{
    "my-keyset": {
        "my-key": {
            "one": "you have one apple",
            "some": "you have apples for the day",
            "many": "you have enough apples to last a lifetime",
            "none": "you don't have apples my friend"
        }
    }
}
```

```ts
import {useI18n} from '@/src/i18n';

i18n('my-keyset', 'my-key', {count: 5});
```

`count` - специальный параметр для переводов с плюрализацией, но его также можно использовать как параметр в переводах с плюрализацией (например, `У тебя {count} яблок`)

### Интеграция с компонентами:

Например для перевода:

```json
{
    "footer": {
        "copyright": "Copyright {link}. All rights reserved."
    }
}
```

Используем компонент как параметр `i18nRaw`:

```tsx
import {i18nRaw} from '@/src/i18n';

const i18nRaw = useI18nRaw();

i18nRaw('my-keyset', 'my-key', {
    link: <Link url="#" key="key">{i18n('another-keyset', 'yandex')}</Link>
});
```

## Как добавить перевод

* Добавляем в код новый текст:

  ```ts
  i18n('my-keyset', 'my-key', {metro: 'Парк Культуры'});
  ```

* Отправляем новый ключ в танкер:

  ```bash
  falcon tanker --push
  ```

  [Подробнее о командах и что они делают](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md).

* Переходим в [проект в танкере](https://tanker.yandex-team.ru/project/lavka-falcon) и открываем ключ. Добавляем русский перевод (`Метро {metro} находится в той стороне`)

* Справа сверху, рядом с аватаркой, есть знак вопроса. Нажимаем на него, затем в попапе жмем "Заказ перевода"

* В открывшейся форме заполняем поля:
    - Тип задачи - `Перевод`
    - Вид текста - `Интерфейс`
    - ABC сервис - `Лавка / Распознавание накладных`
    - Суть задачи - `Перевод ключей`
    - Инстанс Танкера - `Новый`
    - Ссылки на сущности в Танкере - здесь пишем ссылки на ключи/кейсеты/проект
    - Выбираем исходный язык, языки для перевода и ставим дедлайн
    - Язык перевода - выбираем нужные нам языки (ru,en,fr,he)

* Когда переводы будут готовы, синхронизируемся с танкером:
  ```bash
  falcon tanker --pull
  ```

* Для объединения команд `pull` и `push`, существует
  ```bash
  falcon tanker --sync
  ```

💡 tanker не подтянет переводы если они не подтверждены

💡 tanker не подтянет переводы если функции `i18n` или `i18nRaw` вызываются не в папке `src/client`
