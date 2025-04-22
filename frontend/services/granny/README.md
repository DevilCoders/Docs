# Granny

Бабуля — Серп для старых браузеров!

## Запуск [Hermione] тестов

[Документация](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/)

* Функциональные тесты:
  * [Запуск](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#zapusktestov)
  * Скипы в [TestCop]: https://testcop.si.yandex-team.ru/skips/hermione/granny
* Интеграционные тесты:
  * [Запуск](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#zapuskintegracionnyxtestov)
  * Скипы в [TestCop]: https://testcop.si.yandex-team.ru/skips/hermione-e2e/granny

Перед первым запуском необходимо настроить [Qloud-прокси](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/qloud-proxy/)

## Описания тестовых сценариев (YML)

[Документация palmsync][Palmsync]

[Документация manual-runs][manual-runs]

Тестовые сценарии хранятся в `*.testpalm.yml`-файлах в папке [features](.features) и
синхронизируются с проектом [granny-js](https://testpalm.yandex-team.ru/granny-js) на сервисе TestPalm.

Валидация правильности заполнения файлов с тестовыми сценариями и их синхронизация выполняются инструментом [Palmsync].

[Palmsync] для проекта настроен через конфигурационный файл [`.palsync.conf.js`].
Он содержит настройки [Palmsync], специфичные для проекта. Подробнее о структуре конфигурационного файла можно прочитать
в документации [Palmsync] [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/README.md#конфигурация-с-помощью-файла-palmsyncconfjs).

### Кастомные поля проекта

О том, как настраивать кастомные поля, можно прочитать в документации [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/README.md#schemeextension).
Настроенные в настоящий момент кастомные поля перечислены ниже.

#### category

Категория тестируемой фичи.

#### v-team

Ответственная команда.

Допустимые значения можно увидеть в описании этого поля в конфигурационном файле [Palmsync] - [`.palsync.conf.js`].

#### regions

Объект из пар `имя домена: регион`. Актуальный регион для заданного домена. Пример:

```yaml
regions:
  ru: 213
  by: 157
  kz: 163
  ua: 143
  com.tr: 11508
  com: 87
```

#### selector

Селектор, по которому можно найти функциональность на странице

#### deprecated

Поле для неактуальных фичей, которые уже не будут показываться пользователям, но не выпилены из кода.
Поле содержит ссылку(и) на таск на отрыв фичи в формате https://st.yandex-team.ru/SERP-NNNNN.

#### requests

Запросы по умолчанию для каждого домена. Пример:

```yaml
requests:
  ru: 'пробки бирюлево'
  by: 'улица карла маркса пробки'
  kz: 'пробки проспект абая'
  ua: 'пробки бульвар шевченко'
  com.tr: 'Teşvikiye Caddesi trafik'
```

#### browsers

Список браузеров, для которых актуален сценарий. На проекте добавлена валидация поля: каждое значение, указанное в поле,
должно быть одним из названий браузеров, описанных в [`browsers.js`].

В остальном полностью соответствует описанию поля в [общей схеме](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/README.md#browsers).

[Hermione]: https://github.com/gemini-testing/hermione
[Palmsync]: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/palmsync
[TestCop]: https://github.yandex-team.ru/search-interfaces/testcop

[`.palmsync.conf.js`]: ./.palmsync.conf.js
[`browsers.js`]: ./browsers.js
