# Пишем тесты

- [Установка зависимостей](#setup)
- [Написание тестового сценария](#plan)
- [Написание теста](#write)
- [Запуск написанного теста](#run)

## Установка зависимостей { #setup }

Для запуска тестов на локальном селениуме в системе должны быть установлена Java Development Kit 8. Фронтенд разработчикам для этого было бы удобно воспользоваться сервисом [SdkMan](https://sdkman.io/):

- Установите `sdkman` следуя [инструкциям](https://sdkman.io/install)

- Установите Java Development Kit 8, пользуясь `sdkman` (например `sdk install java 8.282.08.1-amzn`)

- Установите остальные зависимости, выполнив `npm ci`

Для локального запуска тестов в системе должен быть установлен Google Chrome 85. Для того чтобы версия оставалась постоянной, необходимо отключить обновления.

- Скачайте Google Chrome [отсюда](https://google-chrome.en.uptodown.com/mac/download/2460182)

- Перед первым запуском отключите обновления, выполнив в терминале:
```
defaults write com.google.Keystone.Agent checkInterval 0

sudo mkdir -p /Library/Google/GoogleSoftwareUpdate
sudo chmod 000 /Library/Google/GoogleSoftwareUpdate
sudo chmod 000 /Library/Google
sudo chown nobody:nogroup /Library/Google/GoogleSoftwareUpdate
sudo chown nobody:nogroup /Library/Google
```

## Написание тестового сценария { #plan }

Перед тем как писать тест необходимо написать тестовый сценарий.

Правила написания тестового сценария:

- файл yml и тестовый файл должны лежать в одной папке и названия должны отличаться только расширением (пример названия файла: для `textCamaigns.hermione.ts` — `textCamaigns.hermione.yml`)
- В yml-файлах используется синтаксис yaml ([подробнее о структуре файла и PalmSync](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/yaml-files.md))
- Поле `feature` в yml-сценарии соответствует верхнему `describe` в тестовом файле
- Дальнейшее описание повторяет иерархию вложенности `describe` `it` из тестового файла
- Описание сценария строится из полей  `-do` `-assert`
- Поле `file` – путь до скомпилированного в js тестового файла. Заполняется при наличии тестов.
- Поле `tags` – тэги для фильтрации в Testpalm. Можно указать как для всего сьюта, так и на любом уровне вложенности вплоть до отдельных кейсов. Тэг `not automated` проставляется в Testpalm автоматически, его добавлять не нужно.

Пример `yml`-файла с описанным тестовым сценарием можно посмотреть по [ссылке](https://github.yandex-team.ru/direct/dna/blob/master/tests/hermione/suites/frozen/editors/cpaStrategyAlerts.view.hermione.yml).

После того как сценарий написан, провалидируйте его, используя команду `npm run palmsync:validate`.

[Подробнее о тестовых сценариях](tests-yml.md)

## Написание теста { #write }

При написании тестов используется шаблон проектирования `Page Object Pattern`.

> [Page Object Pattern](http://internetka.in.ua/selenium-page-object/) — шаблон проектирования, служит для разделения логики выполнения тестов от реализации.

`Page Object`-ы располагаются в директории `tests/page-objects`.
Пример написания теста с применением `Page Object`-а:

Плохо:
```javascript
it('Открываем попап c типом кампании "Тексто-графическое обьявление"', asynс function () {
    await this.browser
        .waitForExist('.add-campaign-control')
        .click('.add-campaign-control')
        .waitForExist('.campaign-types-list__title=Динамические объявления')
        .click('.campaign-types-list__title=Динамические объявления')
        .waitForExist('.frame-edit-popup_loaded');
});
```

Хорошо:
```javascript
it('Открываем попап c типом кампании "Тексто-графическое обьявление"', asynс function () {
    await campaignEditPopup.open(campaignsTypes.text);
});
```

---

В идеале, в тестах должны использоваться только PageObjects.

---

### Создание \ редактирование \ удаление API-сущностей { #on-demand }

Для операций с API-сущностями директа (такими как кампании, группы, объявления) используется специаллизированное API, которое называется `steps-proxy` (степы) [ссылка на определение](tests-main-concepts.md#main-concepts).

#### Как работать со steps-proxy { #steps-proxy-how-to }
Код, который делает запросы в steps-proxy лежит в [`tests/steps`](https://github.yandex-team.ru/direct/dna/tree/master/tests/hermione/steps).

Это набор классов для создания данных на бетах. Они общаются по http с сервисом `api-steps-proxy.qloud.yandex-team.ru`.
Код сервиса можно посмотреть тут [directapi-steps](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/directapi-steps).

К сервису нет документации. Сейчас чтобы добавить новый метод к нам в steps нужно:

- Открыть исходный код и найти публичные методы помеченные аннотацией @steps.
- Понять какие аргументы принимает метод (найти декларацию аргументов, выписать все необходимые поля).
- Сформировать запрос. В запросе указываем имя метода которых хотим вызвать и задаем аргументы с которыми хотим позвать метод. 

Есть тикет с запросом на более удобное API: DIRECT-78302.

## Снятие дампов (только для frozen) { #dump }

Если вы пишите frozen тесты, то необходимо снять дампы.
В начало файла добавьте команду `hermione.dumpster.dump();`.
Затем снимите дампы по [инструкции](how-to-refresh-dumps.md).

## Запуск написанного теста { #run }

Для запуска теста:

- Запустите `selenium`, выполнив команду `npm run selenuim`

- В соседней вкладке выполните запуск теста `BETA_PORT=TS npm run hermione:standalone -- --grep="<test_name>"`. Пример: `BETA_PORT=TS npm run hermione:standalone -- --grep="Кампании: действия У пользователя есть одна кампания Пользователь удаляет кампанию -> грид пуст"`.

Если при запуске теста выясняется, что он не проходит, понять причину поможет расстановка в коде теста `await this.browser.debug();`. При выполнении этой команды будет открыт [debug REPL](https://webdriver.io/docs/api/browser/debug).

## Перекрёстные ссылки

- [Доступные переменные окружения](tests-env-variables.md)
- [Как работают тесты под капотом](tests-under-the-hood.md)
- [Какие есть команды для запуска тестов](tests-run.md)
- [Инструкция как снять дампы](how-to-refresh-dumps.md)
