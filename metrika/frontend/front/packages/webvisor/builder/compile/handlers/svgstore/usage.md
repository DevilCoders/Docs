# Обработчик SVG

Данный обработчик занимается сборкой SVG-спрайтов, их оптимизацией и сжатием. Обработчик использует пакеты `svgstore` и `svgo` для работы.

# Пример

```javascript
exports.svgstore   = {
  prefix: 'wv-',
  options: {
    inline: true
  },
  svgo: {
    js2svg: {
      pretty: true,
    },
    plugins: [
      { "removeXMLNS": true },
      { "removeTitle": true },
      { "removeUselessDefs": false },
      { "removeHiddenElems": false },
      { "removeUselessStrokeAndFill": true },
      { "removeAttrs": { "attrs": ["fill", "opacity", "fill-rule"] } }
    ]
  }
}
```

# Параметры настройки обработчика
- entry – путь до файлов SVG, поддерживает glob
- dest – путь до результирующего файла (например, build/images/sprites.svg). Путь указывается полностью, включая имя файла, так как обработчик на выходе имеет единственный файл, состоящий из нескольких SVG файлов, взятых из по путям их параметра `entry`.
- prefix – префикс имен спрайтов. имена формируются по схеме [prefix]-[filename], при этом расширение (.svg) будет удалено из имени спрайта
- options – настройки [svgstore](https://www.npmjs.com/package/svgstore#tostringoptions-string)
- svgo – настройки [SVGO](https://github.com/svg/svgo#what-it-can-do)
