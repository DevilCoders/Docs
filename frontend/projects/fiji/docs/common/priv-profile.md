## Профилирование привов
Пока только вариант для WebStorm.

Рекомендуется ознакомиться со следующими статьями:
* [Node.js profiling in WebStorm. Part 1: CPU profiling](https://blog.jetbrains.com/webstorm/2015/05/node-js-profiling-in-webstorm-part-1-cpu-profiling/)
* [Node.js profiling in WebStorm. Part 2: Memory profiling.](https://blog.jetbrains.com/webstorm/2015/07/node-js-profiling-in-webstorm-part-2-memory-profiling/)

### Подготовка данных
Чтобы запустить наши привы, нам необходимо получить JSON с результатами поиска:
```bash
wget -O images_request.json "https://yandex.ru/images/search?text=bmw&export=json"
wget -O video_request.json "https://yandex.ru/video/search?text=bmw&export=json"
```

### Скрипт для профилирования
Вся логика находится в [profile.js](../profile.js). Внутри файла нужно поправить две переменных:

```js
const template = path.resolve('project/desktop/pages/common/common.renderer.js');
const request = path.resolve('export.json');
```

где `template` — путь до нужного прива, `request` — данные, полученные с помощью `wget`.

### Запуск
* добавляем конфигурацию для профилирования `Run -> Edit configurations`
    * выбираем node.js
    * на вкладке V8 profiling выбираем `Record CPU profiling info`
* правкой кнопкой на `profile.js` -> `Run`
