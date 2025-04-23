Содержит форму с настройками визульного оформления и превью.

###Параметры bemjson
- {string} [type] Тип блока internal-content-rtb|internal-context-direct|search-direct, по умолчанию rtb
- {object|array} [value] Значения найтроек, если массив, то из одного объекта, только для передачи из tt2
- {string} js.fieldNamePrefix Префикс полей, которые нужно сохранить на сервере
- {string} error Текст ошибки
- {string} label Название формы

#### Пример value
{
    font_family: '',
    no_sitelinks': '0',
    font_size: '1',
    site_bg_color: 'FFFFFF',
    border_color: '6699CC',
    limit: '3',
    hover_color: '6699CC',
    favicon: '1',
    border_radius: '1',
    header_bg_color: '6699CC',
    url_color: '006699',
    title_font_size: '3',
    title_color: '006699',
    bg_color: 'CCEEFF',
    type: 'vertical',
    border_type: 'block',
    text_color: '000000'
}

#### Пример js.fieldNamePrefix
'appearance__'
