### Tanker kit

Все файлы с переводами находятся в src/translations

Имя кейсетов в танкере соответствует названию папки внутри translations

Например:

```
   'translations/Header/ru.js' -> 'Header'
```

Чтобы использовать утилиту tanker установите tanker-cli:
`sudo npm i tanker-cli -g --registry http://npm.yandex-team.ru`

Также необходимо добавить переменную окружения TANKER_TOKEN.
Для получения OAuth токена авторизуйтесь в браузере от имени необходимого пользователя и перейдите по ссылке https://nda.ya.ru/3SjQY7.
Также у вас должны быть права для редактирования проекта в танкере. Их [можно запросить](https://doc.yandex-team.ru/Tanker/general-info/concepts/quickstart.html#quickstart__idm) в IDM

Чтобы добавить кейсет в танкер надо добавить папку внутри папки 'translations', в папке создать файл с русским переводом (ru.js).
При выгрузке собираются только русские кейсеты (translations/ru.js)

#### Команды

`tanker-push` - выгрузка локальных кейсетов в танкер

`tanker-pull` - выгрузка кейсетов из танкера

Более подробно можно ознакомиться в описании тулзы [tanker-kit](https://github.yandex-team.ru/search-interfaces/frontend/blob/f5b00cb03d009996a9744b81617123871d3a0b4f/packages/tanker-kit/doc/overview.md)
