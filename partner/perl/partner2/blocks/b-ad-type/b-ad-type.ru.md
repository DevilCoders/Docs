Позволяет выбрать количество блоков, для типов, где есть минимальное и максимальное количество блоков.

###Параметры bemjson
- {array} js.types Список типов блоков и их параметров

Пример списка типов:

[
    {'name':'horizontal', 'caption':'Горизонтальный (1-4 объявлений)', 'id':'horizontal', 'max_banners':'4', 'min_banners':'1'},
    {'name':'vertical', 'caption':'Вертикальный (1-9 объявлений)', 'id':'vertical', 'max_banners':'9', 'min_banners':'1'},
    {'name':'fixed', 'caption':'Фиксированный', 'types':[
        {'name':'fixed-vertical', 'caption':'Фиксированный вертикальный', 'types':[
            {'name':'160x600', 'banners':'5', 'caption':'160x600 (5 объявлений)', 'id':'160x600'},
            {'name':'240x400', 'banners':'5', 'caption':'240x400 (5 объявлений)', 'id':'240x400'},
            {'name':'120x600', 'banners':'4', 'caption':'120x600 (4 объявления)', 'id':'120x600'},
            {'name':'200x300', 'banners':'3', 'caption':'200x300 (3 объявления)', 'id':'200x300'},
            {'name':'120x240', 'banners':'2', 'caption':'120x240 (2 объявления)', 'id':'120x240'}
        ]},
        {'name':'fixed-square', 'caption':'Фиксированный квадратный', 'types':[
            {'name':'300x300', 'banners':'4', 'caption':'300x300 (4 объявления)', 'id':'300x300'},
            {'name':'300x250', 'banners':'3', 'caption':'300x250 (3 объявления)', 'id':'300x250'},
            {'name':'250x250', 'banners':'3', 'caption':'250x250 (3 объявления)', 'id':'250x250'},
            {'name':'180x150', 'banners':'1', 'caption':'180x150 (1 объявление)', 'id':'180x150'},
            {'name':'125x125', 'banners':'1', 'caption':'125x125 (1 объявление)', 'id':'125x125'}
        ]},
        {'name':'fixed-horizontal', 'caption':'Фиксированный горизонтальный', 'types':[
            {'name':'728x90', 'banners':'3', 'caption':'728x90 (3 объявления)', 'id':'728x90'},
            {'name':'600x60', 'banners':'2', 'caption':'600x60 (2 объявления)', 'id':'600x60'},
            {'name':'468x60', 'banners':'1', 'caption':'468x60 (1 объявление)', 'id':'468x60'},
            {'name':'234x60', 'banners':'1', 'caption':'234x60 (1 объявление)', 'id':'234x60'}
        ]}
    ]}
]
