# yandex-printf

Расширение прототипа строки методами для форматирования из printf.
Работает на основе NPM-модуля [pff](https://npmjs.org/package/pff).

## Установка
```bash
# прописать внутренний npm-репозиторий
echo "registry = http://npm.yandex-team.ru/" >> ~/.npmrc

npm install yandex-printf
```

## Использование

```javascript
var printf = require('yandex-printf');

// Используем напрямую функцию printf
printf("/i/%s/%s/%s/feature.omnibox.%d.jpg", 'ru', 'ru', 'tablet', 2); // "/i/ru/ru/tablet/feature.omnibox.2.jpg"

// Или через функции f и printf из String.prototype
'/i/%s/%s/%s/feature.omnibox.%d.jpg'.f('ru', 'ru', 'tablet', 2);
'/i/%s/%s/%s/feature.omnibox.%d.jpg'.printf('ru', 'ru', 'tablet', 2);
```

```String.prototype.f``` и ```String.prototype.printf``` определяются, только если они не были определены ранее.
