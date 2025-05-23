# Обработчик Stylus файлов

Этот обработчик предназначен для компиляции *.styl файлов, использует пакет `stylus` для работы.

В папке `./plugins` находятся кастомные плагины для Stylus. Все плагины загружаются автоматически перед компиляцией и представляют из себя стандартные stylus-плагины. Подробнее можно прочитать в [документации](http://stylus-lang.com/docs/js.html)

# Пример

```javascript
exports.stylus   = {
  options: {
    linenos: true,
    compress: false
  },
  autoprefixer: {
    browsers: ['last 3 versions', 'ie < 9', 'safari >= 6']
  },
  css_path: require_env().css_path
}
```

# Параметры настройки обработчика

- entry – файлы(ы) для обработки, поддерживает glob
- dest – путь до директории назначения, где будут созданы файлы после компиляции
- options – объект со стандартными настройками stylus из [документации](http://stylus-lang.com/docs/js.html)
- autoprefixer – настройки автопрефиксера (плагин предоставляется из коробки)
- css_path – настройка плагина [image-url](./plugins/image-url.js), в зависимости от окружения (NODE_ENV) выбирает корректный адрес для ресурсов (изображения, шрифты) в финальном CSS
