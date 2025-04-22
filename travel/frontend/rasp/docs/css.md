# CSS

Для доступа к статичным (не зависящим от версии приложения) картинкам (лежат в папке static/\_/images) в stylus-файлах есть переменная $staticImagesPath:

```stylus
.SomeBlock
    background: url($staticImagesPath + '/loader.gif')
```
