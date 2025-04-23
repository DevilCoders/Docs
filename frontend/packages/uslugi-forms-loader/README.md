# Загрузчик форм для Яндекс.Услуг

## Установка

```bash
$ npm install --save-dev @yandex-int/uslugi-forms-loader
```

## Пример использования

```js
import { UslugiFormsLoader } from '@yandex-int/uslugi-forms-loader';

const loader = new UslugiFormsLoader({
    container: document.querySelector('.evacuator-form'),
    url: 'https://yandex.ru/uslugi-forms/evacuator',
    onMessage(data) {
        // Полученное событие из Iframe
        switch(data.type) {
            case 'ready':
                //...
                break;
            case 'close':
                //...
            default:
                //...
                break;
        }
    },
    onError(error) {
        // Iframe загрузился с ошибкой или не загрузился в течении 30 секунд.
        //...
    }
});

loader.createIframe();

// Отправить событие в Iframe.
loader.sendMessage({
    type: 'setInitialData',
    payload: {
        //...
    },
});

```
