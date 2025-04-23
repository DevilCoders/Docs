# API вызова виджета сохранения ресурса

## Оглавление

 * [Установка](#install)
 * [Подключение в browserify или webpack](#require-of-browserify-or-webpack)
 * [Подключение в browser](#require-of-browser)
 * [Генерация документации для API по jsDoc](#denerating-doc)
 * [Как использовать API](#how-to-use)
   * [Изменения параметров работы API](#change-api-config)
   * [#selectAndSave](#WidgetSaveApi__saveAndMove)
 * [сборка пакета](#build)

## <a name="#install"></a>Установка

```bash
npm install && npm run build
```

## <a name="require-of-browserify-or-webpack"></a>Подключение в browserify или webpack

```javascript
var WidgetSaveApi = require('widget-save-api');
```

## <a name="require-of-browser"></a>Подключение в browser

```html
<script type="text/javascript" src="dst/widget-save-api.min.js" />
```

для отладки, можно подключить неминифицированный файл

```html
<script type="text/javascript" src="dst/widget-save-api.js" />
```

## <a name="denerating-doc"></a>Генерация документации для API по jsDoc

```bash
npm run doc
```

В ней описаны методы API и их применение.


## <a name="how-to-use"></a>Как использовать API

Предположим, что `widget-save-api` уже подключено и доступно в глобальной области видимости через переменную `WidgetSaveApi`

### <a name="change-api-config"></a>Изменения параметров работы API

Во время отладки приложения может появиться необходимость установить отладочные ссылки ручки `save` (например, `dev`) . Для этого у API есть свойство `config`, в котором определены конфигурационные данные:

 - `origin` - домен вместе с протоколом, где размещается ручка `save`.
 - `saveUrl` - полный путь к ручке `save`.
 - `moveUrl` - полный путь к ручке `move`.
 - `dialogUrl` - полный путь к странице Виджета сохранения на Диск.

### <a name="WidgetSaveApi__saveAndMove"></a>
#SaveAndMove
Основная работа с виджетом предполагает следующий сценарий. Вызывается метод `WidgetSaveApi.saveAndMove`, в который передаются необходимые параметры. Во время вызова сразу начинается сохранение файла пользователю на диск в папку Загрузки (название папки зависит от языка пользователя). Следующий шаг - вызов метода `onSuccess` или `onError`, которые были переданы в качестве параметров. После этого при успешном сохранении пользователь может также переместить файл внутри диска. При перемещении будет вызвана функция `onMove`. При закрытии диалогового окна будет вызвана функция `onClose`. Если произошла ошибка перемещения или при работе с диалогом, то вызовется функция `onError`.


Пример использования метода
```javascript
      WidgetSaveApi.saveAndMove({
          sourceId: 'resource id',
          fileName: 'name',
          sk: 'uf9fdf814948c5a83520cca4f83c45433',
          uid: '0000000',

          container: document.body,
          width: 500,
          height: 400
      }, {
          onSuccess: function(data) {
            // ресурс успешно сохранен
          },
          onClose: function() {
            // необходимо закрыть диалоговое окно

            console.log('close', arguments)
          },
          onError: function() {
            // произошла ошибка при сохранении или перемещении
            console.log('error', arguments)
          },
          onMove: function(data) {
            // пользователь переместил файл
            console.log(arguments);
            document.body.innerHTML = 'moved ' + data.name  +' to <a href="' + data.url + '">' + data.dirname + '</a>'
          }
      });
```
## <a name="#build"></a>Сборка пакета
чтобы собрать пакет, нужно выполнить
```sh
	npm run deb
```
