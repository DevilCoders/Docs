
# Танкер

[Проект в Танкере](https://tanker-beta.yandex-team.ru/project/lavka-pigeon)

Танкер использует `OAuth-токен` для авторизации к своему API. Для генерации персонального токена перейдите по ссылке https://nda.ya.ru/3SjQY7. Затем экспортируйте ключ в ваш `$HOME/.profile` (или `.bash_profile`, если не сработало), добавив
``` bash
export TANKER_API_TOKEN="Тут ваш OAuth токен для Танкера"
```

Для синхронизации переводов используется [tanker-kit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md).
`.tanker` - это служебный каталог, в котором хранятся конфигурационный файл для `tanker-kit`, парсер, диспатчер.

## Использование

``` ts
import {useI18n} from '@/src/i18n';

const i18n = useI18n();

// Параметры объявляются в синтаксисе схожем с параметрами для template strings.
i18n('Keyset', 'Hello {data}', {data: 'world'});

// Плюрализация
i18n('Keyset1', '{count} days', {count: 5, plural: true});

// Интеграция с компонентами
import {i18nRaw} from '@/src/i18n';

const i18nRaw = useI18nRaw();

i18nRaw('Keyset2', 'Hello {data}', {
    link: <Link url="#" key="key">{i18n('Keyset2', 'world')}</Link>
});
```

## Как добавить перевод
* Добавляем в код новый текст
``` ts
i18n('Keyset', `You can't localize the attribute {key}`, {key: 'Barcode'});
```

В ключах пишем только на английском. Это будет фолбек на случай отсутствия соответствующего перевода.
* Отправляем новый ключ в танкер
``` bash
pigeon tanker --push
```
[Подробнее о командах и что они делают](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md)

* Переходим в [проект в танкере](https://tanker-beta.yandex-team.ru/project/lavka-pigeon), открываем ключ и добавляем русский перевод

* Запускаем команду, она выведет кейсеты, в которых есть ключи без переводов
```bash
pigeon tanker check
```

* Заказываем переводы: переходим в [таксишную очередь задач на переводы](https://st.yandex-team.ru/TAXILOC/order:updated:false/filter?resolution=empty()&type=2&status=open&tags=taxi_daily) и в комментах указываем ссылки на кейсеты


* Когда переводы будут готовы, подтягиваем их из танкера
```bash
pigeon tanker --pull
```

* Для объединения команд `pull` и `push`, существует
```bash
pigeon tanker --sync
```
