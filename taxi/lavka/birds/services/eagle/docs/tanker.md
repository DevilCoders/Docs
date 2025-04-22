
# Танкер

[Проект в Танкере](https://tanker-beta.yandex-team.ru/project/lavka-eagle)

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
eagle tanker --push
```
[Подробнее о командах и что они делают](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md)

* Переходим в проект в Танкере и открываем ключ. Добавляем русский перевод

* Переходим в [проект в танкере](https://tanker-beta.yandex-team.ru/project/lavka-eagle)

* Справа сверху, рядом с аватаркой, есть знак вопроса. Нажимаем на него, затем в попапе жмем "Заказ перевода"

* В открывшейся форме заполняем поля:
    - Тип задачи - `Перевод`
    - Вид текста - `Интерфейс`
    - ABC сервис - `Лавка / PIM-система (Орёл)`
    - ЦФО - `YTM192`
    - Суть задачи - `Перевод ключей`
    - Инстанс Танкера - `Новый`
    - Ссылки на сущности в Танкере - здесь пишем ссылки на ключи/кейсеты/проект
    - Выбираем исходный язык, языки для перевода и ставим дедлайн

* Когда переводы будут готовы, подтягиваем их из танкера
```bash
eagle tanker --pull
```

* Для объединения команд `pull` и `push`, существует
```bash
eagle tanker --sync
```
