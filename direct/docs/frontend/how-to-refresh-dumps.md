# Обновление тестовых дампов в DNA
Теоретическая справка [здесь](tests-under-the-hood.md)

## Как понять, что тест упал из-за дампов

Тесты, использующие дампы, запускаются в пул-реквестах в секции `frozen` — падения из-за дампов могут быть только в этой секции.

"Ошибка загрузки" на скриншоте говорит об ошибке бэкенда (или ошибке маппинга ответа).

{% cut "Пример скриншота" %}

![скриншот ошибки](./assets/test-dump-error.png)

{% endcut %}

Соответственно, такая ошибка в случае задампленного теста говорит о том, что дамп протух, и нужно его обновить.
Если по какой-то причине есть сомнения, что тест использует дампы, дополнительно можно проверить, что тест дампится через клемент, это можно проверить в коде. Такой тест отмечен специальной декларацией `hermione.dumpster.dump()` (декларацией может быть отмечен сам тест, или describe, в котором он содержится)

## Как переснимать дампы

{% note warning %}

Так как падения были в пул-реквесте, нельзя обновлять дампы на ТС. Вместо ТС нужно использовать одну из единых бет, как это происходит в CI. Чтобы запускать тесты на единых бетах, нужно запускать гермиону с флагом `OVERRIDE_HASHSUMS=1`

{% endnote %}

Так как тесты для снятия дампов запускаются с флагом `OVERRIDE_HASHSUMS` — нужно подготовить правильную версию статики, для этого можно использовать команду `npm run deploy`, чтобы загрузить статику того коммита, на котором мы находимся.

Наконец, чтобы снять дампы, нужно запустить гермиону с клементом в режиме записи с флагом `--save`.

Если в пул-реквесте упало большое количество тестов, то имеет смысл запустить гермиону в интерактивном режиме с отображением результатов падений в пул-реквесте. Для этого нужно сначала выгрузить из SANDBOX'а отчет с падениями

`npm run reuse-report <sandbox task id>`
[как найти sandbox task id](tests-reuse-report.md)

После чего можно запустить гермионы с указанием нужного сета тестов и запустить упавшие тесты

`npm run hermione gui -- --save --set frozen`

{% note info %}

Во время записи дампов в консоль выводится debug лог, в котором написано, будто бы запрос проксируется на `test-direct.yandex.ru`. Этого не нужно пугаться, запросы на самом деле проксируются на единую бету, просто для консистентной записи дампов в запросе подменяется заголовок host, по которому определяется, в какой файл будет сохранен дамп

{% endnote %}

После того, как дампы обновлены, нужно запустить клемент в режиме чтения (`--play`) и проверить, что тесты успешно выполняются

## TL;DR { #tldr }

Например, обновляем дампы в ветке users/your-login/DIRECT-XXX-some-branch:

```bash
arc checkout users/your-login/DIRECT-XXX-some-branch
```

### Одной командой

Команда скачивает статику, получает готовый frozen-отчет из sandbox-задачи и запускает gui гермионы в режиме сохранения дампов.
Далее нужно или принять скриншоты, которые протухли или перезапустить упавшие тесты (если ошибка в дампах).
```bash
pnpm run hermione:refresh ссылка_на_отчёт (https://proxy.sandbox.yandex-team.ru/2797062705/report-hermione:ci/index.html)  
```

### То же самое, но руками

Получаем свежую версию статики:

```bash
npm run deploy
```

Дальше может быть два варианта запуска гермионы: c гуи и без. Если не нужно переснимать скриншоты – то гуи не пригодится.

Без GUI: запускаем гермиону в режиме записи с грепом конкретных тестов, чтобы не мешали остальные, в неинтерактивном режиме

```bash
OVERRIDE_HASHSUMS=1 npm run hermione -- --save --grep $GREP
```

Или запускаем гермиону в интерактивном режиме c указанием набора frozen тестов. Ранее выгруженный отчет поможет понять, какие конкретно тесты нужно перезапустить:

```bash
OVERRIDE_HASHSUMS=1 npm run hermione gui -- --save --set frozen --from=ссылка_на_отчёт (https://proxy.sandbox.yandex-team.ru/2797062705/report-hermione:ci/index.html)
```

Прогоняем тесты еще раз, в режиме чтения, чтобы проверить, что все прошло:

```bash
OVERRIDE_HASHSUMS=1 npm run hermione gui -- --play --set frozen
```

## Проблема записи дампов на MacOS { #macos-troubles }

Если в логи попал такой текст:
```log
2021-05-25T14:41:58.017Z stderr 2021-05-25T14:41:58.017Z si:archon:cli Finish extend with commands
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'LIBARCHIVE.creationtime'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.dev'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.ino'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.nlink'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.dev'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.ino'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.nlink'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.dev'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.ino'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.nlink'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.dev'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.ino'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.nlink'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'LIBARCHIVE.creationtime'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.dev'
2021-05-25T14:41:58.255Z stderr tar: Ignoring unknown extended header keyword 'SCHILY.ino'
```

То самым простым решением будет скачать gnu-tar:

```
brew install gnu-tar
```

И после разархивировать и сархивировать обратно дампы:

```sh
tar -xvzf tests/tests-dumps.tar.gz
# ВАЖНО! запускаем именно gnu-tar (gtar)
gtar -zcf tests/tests-dumps.tar.gz tests/dumps
```

Команда, после которой такой проблемы больше не будет:

```sh
sudo unlink `which tar`
sudo ln -s `which gtar` /usr/bin/tar
```

Чтобы восстановить исходный tar-файл на bsdtar, поставляемый с MacOS, замените из предыдущей команды ```which gtar``` на ```which bsdtar```:

```sh
sudo unlink `which tar`
sudo ln -s `which bsdtar` /usr/bin/tar
```
