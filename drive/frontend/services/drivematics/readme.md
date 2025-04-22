# Drivematics

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=drive/frontend/services/drivematics&vcs=arc)](https://oko.yandex-team.ru/arc/drive/frontend/services/drivematics)

- [Как развернуть](#start-guide)
- [Процесс разработки](#development)
- [Live templates](#live-templates)
- [Storybook](#storybook)
- [Hermione](#hermione)
- [Unit-тестирование](#unit-testing)

## <a name="start-guide"></a>Как развернуть

1. Установить arc клиент https://docs.yandex-team.ru/devtools/intro/quick-start-guide

2. Примонтировать репозиторий arcadia:

   ```shell script
   mkdir -p arc && cd arc
   mkdir -p arcadia store
   arc mount -m arcadia/ -S store/
   cd arcadia/drive/frontend/services/drivematics/
   ```

   После перезагрузки системы повторять только 2 последних шага:

   ```shell script
   arc mount -m arcadia/ -S store/
   cd arcadia/drive/frontend/services/drivematics/
   ```

3. Установка зависимостей

   Требуются:

   - [nvm](https://github.com/nvm-sh/nvm) - управление версиями NodeJS

   ```shell script
    nvm install
    npm ci
   ```

4. Добавить в `/etc/hosts` следующие записи

   ```shell script
   127.0.0.1 localhost.yandex.ru
   127.0.0.1 localhost.yandex.com
   127.0.0.1 localhost.vlootkit.com
   ```

5. Для корректной работы генерации фикстур тестов необходимо получить [oauth token](https://oauth.yandex.ru/authorize?response_type=token&client_id=ee2a628eb96d40a9807fe7d57b357474)
   Результат положить в `./secrets/oauth`

6. Запуск сервера разработки

   Drivematics https://localhost.yandex.ru:8000

   ```shell script
   npm run start:drivematics:testing
   npm run start:drivematics:prestable
   npm run start:drivematics:prod
   ```

   Vlootkit https://localhost.vlootkit.com:8000

   ```shell script
   npm run start:vlootkit:testing
   npm run start:vlootkit:prestable
   npm run start:vlootkit:prod
   ```

   Для нормальной работы vlooktit домена нужно добавить в доверенные корневой сертификат:

   ```shell script
   sudo security add-trusted-cert -d -r trustRoot -k "/Library/Keychains/System.keychain" VlootkitCA.pem
   ```

## <a name="development"></a>Процесс разработки

```shell script
arc pull trunk
arc checkout -b feature_branch_name.DRIVEMATICSDEV-123
...
arc commit -a -m "feat(drivematics): DRIVEMATICSDEV-123 feature branch short description"
arc pr create --push
```

В имени коммита необходимо указывать правильный тип задачи:

- `feat` — добавлена новая функциональность / новые компоненты / страницы и т.д.
- `fix` — исправлен баг в клиентском коде
- `docs` – добавлена документация кода, JSDoc и `*.md` файлы с документацией по проекту
- `style` – исправлены стилистические ошибки: пробелы, точки с запятой и прочее форматирование, которое не затрагивает сам код
- `refactor` — переработана часть кода. Все, что нельзя отнести ни к `feat`, ни к `fix`. Направлены на улучшение читаемости и поддерживаемости кода.
- `perf` — схожа с `refactor`, но изменения направлены на улучшение производительности кода
- `test` — добавлены или изменены тесты
- `chore` — произведены изменения в служебных файлах, конфигурациях, и прочему коду, который влияет только на процесс разработки и сборки проекта

После коммита должен запускаться pre-commit hook. Если не запускается, необходимо выполнить команду:

```shell script
printf "\n[pre-commit-hook \"drive/frontend/services/drivematics\"]\n    arctic-husky-pre-commit = .arc/user_hooks/hooks/pre-commit" >> ~/.arcconfig
```

## <a name="live-templates"></a>Live Templates

Для IntelliJ IDEA в папке `live-templates` находятся настройки с актуальными шаблонами для быстрой разработки.

**Для импорта этих настроек необходимо:**

1. Создать архив всего содержимого папки `settings` (`live-templates/settings/**`)
2. Через меню `Files → Manage IDE Settings → Import Settings` выбрать созданный архив

## <a name="storybook"></a>Storybook

Запуск в режиме разработки:

```shell script
npm run storybook:start
```

Сторибук-тесты лежат в файлах `<component_name>.story.tsx`.

## <a name="hermione"></a>Hermione

Запуск в режиме разработки:

```shell script
npm run test:visual:dev
```

Запуск тестов, содержащих только текст `Button` в названии:

```shell script
npm run test:visual:dev -- --grep Button
```

Запуск тестов или принятие скриншотов на базе отчета, сгенерированного CI:

```shell script
npm run test:visual:dev -- --from <hermione_report_path>
```

## <a name="unit-testing"></a>Unit-тестирование

[Jest CLI Options](https://jestjs.io/docs/cli)

Запуск всех тестов:

```shell script
npm run test:unit
```

Запуск в режиме отслеживания изменений:

```shell script
npm run test:unit:watch
```

Запустить только тесты по шаблону или по имени файла:

```shell script
npm run test:unit -- <template-or-fileName>
```
