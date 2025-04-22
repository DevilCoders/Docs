## Файлы с локализацией должны находиться внутри компонент контейнеров, один файл для одного контейнера.

## locale-loader
Добавлен custom webpack loader для работы с файлами типа ***.locale**

## Использование

1. Создаем файл **${fileName}.locale**
2. В файле **${fileName}.locale** создаем объект с ключами локалей
```javascript
{
    en: {
        TEST: 'Text in English'
    },
    ru: {
        TEST: 'Текст на русском'
    }
}
```
3. Импортируем в компоненту , где хотим получить перевод
```javascript
import Message from './${fileName}.locale';

<Message id="TEST" /> // as React Component
Message({id: "TEST"}) // as function
```