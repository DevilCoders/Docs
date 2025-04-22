metrika-contrib
===============

Common blocks for metrika frontend projects

## Publish
Если вы обновляете что-то здесь, нужно запаблишить этот пакет в наш npm репозиторий. Это связано с особенностями текущих сборок. Для паблиша выполните из корня:
`npx lerna version minor`
`cd packages/bem-contrib && npm publish`
Ну и в конце всё что обновилось нужно запушить.

## Переводы
Переводы для bem-contrib хранятся в Танкере вместе с переводами для [metrika-components](https://tanker.yandex-team.ru/?project=metrika-components&branch=master). Сделали так, чтобы не заводить отдельный проект для Танкера.

Переводы блоков из bem-contrib **должны быть помечены** специальным префиксом `bem-contrib:`, чтобы разделять кейсеты для bem-contrib и metrika-components. Например, кейсет для b-page будет выглядеть в Танкере так: `bem-contrib:blocks:common:b-page`.

Для обновления переводов запустить из корня проекта:

```
npx lerna run i18n --scope=@metrika/bem-contrib
```
