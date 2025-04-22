# Тестовые сценарии

Тестовые сценарии описываются в `yml`-файлах. Это относится как к уже написанным тестам, так и к тем, которые планируется написать.

Пример `yml`-файла с описанным тестовым сценарием можно посмотреть по [ссылке](https://github.yandex-team.ru/direct/dna/blob/master/tests/hermione/suites/frozen/editors/cpaStrategyAlerts.view.hermione.yml).

## Зачем писать
Описание сценариев в yml-файлах нужно, чтобы синхронизировать тесты с [Testpalm](https://testpalm2.yandex-team.ru/dna) при помощи [palmsync](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/quick-start.md). Также, описанные в yml сценарии, на которые ещё не написаны тесты – это подробное описание задачи на написание этих тестов.

## Правила написания

- файл yml и тестовый файл должны лежать в одной папке и названия должны отличаться только расширением (пример названия файла: для `textCamaigns.hermione.ts` — `textCamaigns.hermione.yml`)
- В yml-файлах используется синтаксис yaml ([подробнее тут](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/yaml-files.md))
- Поле `feature` в yml-сценарии соответствует верхнему `describe` в тестовом файле
- Дальнейшее описание повторяет иерархию вложенности `describe` `it` из тестового файла
- Описание сценария строится из полей  `-do` `-assert`
- Поле `file` – путь до скомпилированного в js тестового файла. Заполняется при наличии тестов.
- Поле `tags` – тэги для фильтрации в Testpalm. Можно указать как для всего сьюта, так и на любом уровне вложенности вплоть до отдельных кейсов. Тэг `not automated` проставляется в Testpalm автоматически, его добавлять не нужно. [Список доступных тегов](https://github.yandex-team.ru/direct/dna/blob/master/.ci/palmsync/whitelist-tags.js).
- Поле `automation` - в данное поле вносится задача из стартрека.

## Команды
- `npm run palmsync:validate` – запускает валидацию yml-файлов в DNA. Проверяется синтаксис yml-файлов и соответствие тестовых файлов их yml-описаниям. Проверка соответствия проверяет только то, что для теста есть описание с тем же названием в нужном файле, а так же [теги](https://github.yandex-team.ru/direct/dna/blob/master/.ci/palmsync/whitelist-tags.js). Сам сценарий не проверяется.
- `npm run palmsync:sync` – запускает синхронизацию тестов с [Testpalm](https://testpalm2.yandex-team.ru/dna). Для запуска потребуются [установленные из секретницы секреты Искорки](https://github.yandex-team.ru/twilight/twilight-secrets#установка). Запускать синхронизацию с Testpalm рекомендуется только из мастера.

## CI
Для проверки соответствия тестов их yml-описаниям в пулл-реквестах автоматически запускается проверка `Palmsync validate test yml`.
Если в вашем ПР упала эта проверка – нужно пойти в логи sandbox-таски, посмотреть найденные валидатором ошибки и исправить соответствующие тесты или yml-файлы.
