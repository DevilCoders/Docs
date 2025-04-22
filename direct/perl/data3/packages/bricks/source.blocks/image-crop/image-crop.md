#image-crop#

##Описание##
Блок-обертка над i-jquery__crop

###Меинтейнеры###
[ngraf](https://staff.yandex-team.ru/ngraf)

##Пример##
```javascript
    BEM.blocks['image-crop']
        .create(this.findElem('image'), { previewUrl: 'http://****.jpeg'})
        .then(function(imageCrop) {
            imageCrop.getBounds();
        })
```
