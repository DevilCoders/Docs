# hermione-assert-view-hide-scrollbars

Hermione плагин для скрытия скроллбаров на скриншотах в touch браузерах.
Оторвать после решения задачи: https://st.yandex-team.ru/FEI-11218.

## Установка

```
npm i @yandex-int/hermione-assert-view-hide-scrollbars --registry=http://npm.yandex-team.ru
```

## Использование

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-assert-view-hide-scrollbars': {
            enabled: true,
            browsers: ['chrome-pad', 'iphone', 'chrome-phone', 'searchapp']
        }
    },

    // ...
}
```

## Опции

| Опция | По умолчанию | Описание |
| --- | --- | --- |
| `enebled` | `false` | Опция для удобного включения/выключения плагина. |
| `browsers` | | Массив браузеров, в которых нужно скрывать скроллбары. |
| `screenshotDelayMinimum` | `600` | Минимальное значение опции `screenshotDelay` для заданных браузеров, чтобы скрыть скроллбары на скриншотах. Не влияет на значения, переданные через опцию `screenshotDelay` в `assertView`. |
