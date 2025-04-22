#banner-image-crop#

##Описание##
Блок обрезки изображения для баннера

###Меинтейнеры###
[ngraf](https://staff.yandex-team.ru/ngraf)
[dima117a](https://staff.yandex-team.ru/dima117a)

##Пример##
```javascript
{
    block: 'banner-image-crop',
    mods: {
        type: 'single'
    },
    mix: {
        block: 'b-pic-selector',
        elem: 'crop'
    },
    type: 'mobile-content'
}
```
```javascript
this.findBlockInside('banner-image-crop')
    .init({
        previewUrl: 'http://....',
        editorWidth: 200,
        editorHeight: 100,
        origImageWidth: 400,
        origImageHeight: 200
    });
```
