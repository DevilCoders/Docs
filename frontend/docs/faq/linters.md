# Линтеры

В монорепозитории статическая проверка кода настроена централизованно, в корне. Используются инструменты `husky` и `lint-staged`. Набор проверок описан в конфиге [.lintstagedrc.js](../../.lintstagedrc.js).
В конвейере запускаются те же проверки на все измененные файлы. Проверка является обязательной.

N.B. В корне используется пакет [@yandex-int/lint](https://a.yandex-team.ru/arc_vcs/frontend/packages/lint/README.md). Можно подключать пакет в свой сервис, если он еще не в монорепозитории.
Для расширения базовых правил монорепозитория нужно переопределить соответствующий конфиг на уровне сервиса/пакета, унаследовав его от базового [eslint](../../.eslintrc.js) или [stylelint](../../.stylelintrc.json) конфигов. Плагины для eslint нужно устанавливать на уровне сервиса/пакета.

## Локальный запуск

- проверить staged-файлы из корня монорепозитория (работает только с arc): `npm run lint`
- проверить staged-файлы из листа (работает только с arc): `npm run lint --prefix='../..'`
- запустить eslint на всю папку целиком из корня: `npx eslint --quiet --ext .js,.jsx,.ts,.tsx services/stub`

При локальном запуске командой `npm run lint` из корня линтеры eslint и stylelint запускаются с опцией `--fix`.

Т.к. для локальной проверки линтеров используется `lint-staged`, он не поддерживает линтиг partially staged-файлов ([задача](https://st.yandex-team.ru/ARC-3188)) и совсем не линтит untracked-изменения, поэтому перед локальным запуском линтеров нужно добавить все необходимые файлы в stage командой `arc add [PATH ...]`.

# Как подключить husky + lint-staged в проекте

В данном решении прекоммит хук и соотвественно list-staged запускается после рутового монорепного.
Правильный способ запуска lint-staged в проекте [разрабатывается тут](https://st.yandex-team.ru/FEI-21151)

1. Переходим в директорию вашего проекта
2. Устанавливаем пакеты

```bash
npm i -D @yandex-int/lint-staged @yandex-int/si.ci.arctic-husky
```

3. Создаем файл `.lintstagedrc.js` в корне проекта

```js
// конфиг аналогичен оригинальному lint-staged (https://github.com/okonet/lint-staged)
module.exports = {
  "*.{js,ts,tsx,css,md,yml,yaml}": ["prettier --write"],
  "*.css": ["stylelint --fix"]
};
```

4. Создаем файл `.huskyrc.js` в корне проекта

```js
// конфиг аналогичен оригинальному husky (https://github.com/typicode/husky)
module.exports = {
  hooks: {
    "pre-commit": "lint-staged --vcs-adapter @yandex-int/si.ci.lint-staged-arc-workflow"
  }
};
```

## Известные проблемы

eslint падает с ошибкой `'React' was used before it was defined on edited code`.

Данная ошибка возникает, если в листе установлены устаревшие версии зависимостей `@typescript-eslint/parser` или `@typescript-eslint/eslint-plugin`. Все устаревшие версии, которые устанавливались явно, были удалены в рамках тикета https://st.yandex-team.ru/FRONTEND-911, но устаревшие версии могут устанавливаться неявно другими пакетами. Общее решение будет реализовано в рамках тикета https://st.yandex-team.ru/FRONTEND-956.

Текущие варианты решения проблемы:
* найти пакет, который приносит устаревшие версии `@typescript-eslint/eslint-plugin` и `@typescript-eslint/parser` и обновить его (правильный способ)
* установить в лист пакеты `@typescript-eslint/eslint-plugin` и `@typescript-eslint/parser` согласно [конфигу depslint](../../.depslint.json) (быстрый, но костыльный способ)
 
