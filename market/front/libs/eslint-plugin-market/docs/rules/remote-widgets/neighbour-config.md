# neighbour-config

Запрещает изменять хосты neighbour в конфигах для правильной работы ремоут виджетов в белом маркете

> Почему?
В процессе разработки может понадобиться подставить хост с девелоперского стенда, если такое уедет в мастер - будут пробелмы
>с отображением ремоут виджетов

## Использование
Для работы правила необходимо добавить правильные хосты в конфигурацию, например:

```json
{
  "remote-widgets/neighbour-config": [
    "error",
    {
        "desktop": {
            "development": "desktop.bluemarket.fslb.beru.ru",
            "testing": "desktop.bluemarket.fslb.beru.ru",
            "production": "beru.ru"
        },
        "touch": {
            "development": "touch.bluemarket.fslb.beru.ru",
            "testing": "touch.bluemarket.fslb.beru.ru",
            "production": "m.beru.ru"
        }
    }
  ]
}
```




## Примеры

Правильные хосты: 

Для десктопа:
 - development: 'desktop.bluemarket.fslb.beru.ru'
 - testing: 'desktop.bluemarket.fslb.beru.ru'
 - production: 'beru.ru'
    
Для тача    
 - development: 'touch.bluemarket.fslb.beru.ru'
 - testing: 'touch.bluemarket.fslb.beru.ru'
 - production: 'm.beru.ru'
    

