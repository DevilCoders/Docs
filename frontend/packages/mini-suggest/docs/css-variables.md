# CSS-переменные (custom-properties)

В проекте используются [css-custom-properties](//caniuse.com/css-variables).<br>
Большинство сервисов имеют более широкую поддержку браузеров, поэтому мы не можем использовать их без фоллбэков.<br>
На этапе сборка проекта мы [процессим](//a.yandex-team.ru/arcadia/frontend/packages/mini-suggest/.config/.enb/techs/css-variables.js) переменные с помощью `postcss-плагина` [postcss-custon-properties](//github.com/postcss/postcss-custom-properties), возможны три варианта:<br>
1. На проекте нет цветовых тем (светлая\темная и т.д.), тогда мы заменяем переменные на `hex-цвета`. Оставлять `custom-properties` нет смысла т.к. это увеличит размер статики. [Пример](//a.yandex-team.ru/arcadia/frontend/packages/mini-suggest/build/bundles/goods/desktop/mini-suggest/colors.config.js).
2. Проект имеет цветовые темы и `ограниченную поддержку браузеров`, тогда мы можем оставить переменные и сгенерировать в начало стилей определения переменных под каждую тему. [Пример](//a.yandex-team.ru/arcadia/frontend/packages/mini-suggest/build/bundles/goods/desktop/mini-suggest/colors.config.js).
3. Проект имеет цветовые темы и `широкую поддержку браузеров`, тогда мы должны добавить `hex-fallback` и сгенерировать в начало стилей определения переменных под каждую тему. [Пример](//a.yandex-team.ru/arcadia/frontend/packages/mini-suggest/build/bundles/serp/desktop/mini-suggest/colors.config.js).

## Особенности реализации

1. Цвета переменных для бандлов хранятся в файлах `colors.config.js` в одной директории с `.bemdecl.js`. Конфиг имеет тип: 
```typescript
  type DefaultColorMap = Record<string, string>;
  type ColorThemesMap = Record<string, DefaultColorMap>;

  type Config = {
    // Имеет ли бандл цветовые темы
    hasColorThemes?: boolean,
    // has-map с определениями цветов для переменных
    map: DefaultColorMap|ColorThemesMap,
  };
```
2. Переменные, которые не будут найдены в конфиге `colors.config.js` будут оставлены в стилях без изменений.
3. <b>ОСТОРОЖНО</b> Плагин `postcss-custom-properties` заменяет использование `custom-properties с нативным фоллбэком` пр. `color: var(--color, red);` на `color: red;`. Чтобы добавить правило в игнор плагина нужно строкой ранее добавить комментарий `/* postcss-custom-properties:ignore next */`.
4. Т.к. на момент написания функционала некоторые сервисы (морда и СЕРП) собирают саджестовый бандл внутри своего репозитория посредством `enb` нам необходимо добавить `css-фоллбэки` в исходных `.css` файлах. Мы делаем это на этапе `prepublish` после сборки бандлов. [Код](//a.yandex-team.ru/arcadia/frontend/packages/mini-suggest/tools/create-custom-properties-fallbacks.js).
5. Переменные одного и того же сервиса для разных платформ (`desktop, touch`) могу отличаться, поэтому нам приходится резолвить `common` уровень десктопными переменными, а на `touch` уровне дублировать эти правила, чтобы переопределить их.
6. Переменные могут быть как заданы вручную для отдельного бандла, так и импортированы из внешнего пакета пр. `@yandex-serp-design/search-light`, `@yandex-serp-design/search-light`.
