# WebpackMainTemplate plugin

Переопределяет формирование основного шаблона загрузки (то из чего состоит manifest.js)

Добавляет несколько новых функций:

### chunkRetryCount
  Настройка перезапроса чанков для конфига вебпака
  ```json
  output: {
      ...
      chunkRetryCount: 1
  }
  ```
  Целочисленное значение выше нуля.

### Url builder (ub)
  Возможность изменения урла при формировании скрипта в рантайме.
  ```js
  /**
   * @param {Object} installedChunks - текущий набор загруженных и загружаемых чанков
   * @param {Number} chunkId - id текущего чанка
   * @param {String} url - оригинальный url
   * @returns {String} modifiedUrl
   */
  __webpack_require__.ub = function(installedChunks, chunkId, url) { return url; }
  ```

### Script builder (sb)
  Возможность переопределить код, отвечающий за встраивание
  вебпак скриптов на страницу через асинхронный импорт.
  ```js
  /**
   * @param {function} resolve
   * @param {function} reject
   * @param {Object} options
   * @param {Number} options.timeout - таймаут запроса скрипта настраиваемый через webpack конфиг
   * @param {String} options.crossOrigin - режим CORS
   * @param {String} options.nonce - CSP подпись
   * @param {String} options.publicPath - корневая часть сервера статики
   * @param {String} options.srcPath - путь до файла относительно сервера статики
   * @returns {Script} script
   */
  __webpack_require__.sb = function(resolve, reject, options) {}
  ```

### Error handler (eh)
  Возможность переопределить обработчик ошибок загрузки скрипта.
  Сам по себе этот обработчик является новой функциональностью и нужен для ретраев за скриптом.
  Если не хочется потерять встроенный механизм ретраев, то при переопределении стоит так же вызывать базовый код.
  ```js
  /**
   * @param {Object} installedChunks
   * @param {Number} chunkId
   * @param {Error} error
   * @returns {undefined}
   */
  __webpack_require__.eh = function(installedChunks, chunkId, error) {}
  ```

  Пример правильного переопределения:
  ```js
  const originalErrorHandler = __webpack_require__.eh;
  __webpack_require__.eh = function(installedChunks, chunkId, error) {
    // do something else

    originalErrorHandler.call(__webpack_require__, installedChunks, chunkId, error);
  }
  ```
