# Переводы

## Репозиторий:

https://tanker-beta.yandex-team.ru/project/order-history-frontend

## Настройка
Положить токен в перменную окружения `TANKER_TOKEN`

Токен брать [отсюда](https://nda.ya.ru/3SjQY7)
## Выгрузить из танкера

```
tanker pull
```

## Загрузить в танкер

```
tanker sync
```


## Добавление ключа

Если перевод может использоваться в нескольких компонентах, то его стоит положить в `src/client/translations/common.ts` (или в соседний кейсет или создать новый, если в этом есть смысл) и использовать `i18nCommon(keyName)`

В остальных случаях использовать вот так:

```tsx
import * as keyset from '@i18n/Keyset.i18n';
import i18nFactory, { i18nRawFactory } from '@i18n';
import { i18nCommon } from '@translations/common';


const i18n = i18nFactory(keyset);
const i18nRaw = i18nRawFactory(keyset);

const Component = () => (
    <div>
        {i18n('Оплатить')}
        <br>
        {i18nRaw('Подробнее в {help}', {
            help: <a>{i18n('Справке')</a>
        })}
        <button>{i18nCommon('ok')}</buttoon>
    </div>
)

```