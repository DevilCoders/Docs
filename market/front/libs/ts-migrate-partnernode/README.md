# ts-migrate-partnernode

## Установка

Проект собирается с помощью yarn и lerna, если пакеты не установлены, выполните следующую команду.

```bash
   brew install yarn;
   npm i -g lerna;
```

```bash
# устанавливает зависимости в с корневого package.json и в packages/
npm install

# соберет проект и также вложенные пакеты packages/
npm run build

# слинкует пакет в глобальный воркспейс
npm link
```

## Использование

```bash
# в репозитории партнерки
tsm-partnernode --migratePath=./pathToMigrateDir
```

## CLI Options

- `ignoreErrors` - запускает плагин игнора ошибок
- `includeTasks` - перечисление шагов в пайплайне, которые нужно запустить
- `prettier` - прогоняет prettier по сформированным файлам

## Pipeline Tasks

- `gen-files` - генерация конфигурационных файлов и dts
- `flow-to-ts` - миграция кода flow -> ts со сменой расширения
- `npm-config` - обновление npm зависимостей и добавление новых скриптов
- `ts-codemods` - прогоне кодмодов на смигрированном typescript коде

<div align="center">
   <img src="https://jing.yandex-team.ru/files/gus3inov/photo_2020-10-03%2021.55.46.jpeg">
</div>

## Разработка

```bash
npm install

# запуск вотч режима
npm start
```

## Миграция локальных веток на Typescript

Перед релизом тайпскрипта нужно сделать следующее:

1. Сделать бэкап своей локальной ветки (чтобы в случае страшного не потерять своих изменений)

2. Склонировать этот репозиторий и выполнить [инструкции по установке](https://github.yandex-team.ru/market/ts-migrate-partnernode#установка)

3. Смерджить ветку `MARKETPARTNER-16237-launch-pad`

   ```bash
      git merge origin/MARKETPARTNER-16237-launch-pad;
   ```

4. Запустить миграцию
    _пайплайн прогонится только на diff-файлах с мастером._

   ```bash
      NODE_OPTIONS=--max_old_space_size=4096 tsm-partnernode --useDiff --branchForDiff=origin/MARKETPARTNER-16237-launch-pad --includeTasks="npm-config,flow-to-ts,ts-codemodes";
   ```

5. Закоммитить изменения.

6. Обновить зависимости

   ```bash
      veendor install -f;
   ```

7. Обновиться по мастеру, решить конфликты

8. Запустить приттиер и ts-ignore  _может занять некоторое время_

   _если есть желание можно попробовать самому пофиксть ошибки если они будут_


   ```bash
   NODE_OPTIONS=--max_old_space_size=4096 tsm-partnernode --includeTasks="ignore-errors,prettier";
   ```

После миграции могут остаться ts или eslint ошибки, их не должно быть много
Оставшиеся ошибки проще починить руками.

Возможные проблемы:
При сборке проекта с пайплайном миграции у кого-то может возникнуть проблема с необходимостью установить yarn глобально. Саша Моргунов рекомендует делать это через brew https://github.yandex-team.ru/market/ts-migrate-partnernode/pull/39#issuecomment-2395727
