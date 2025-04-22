#show-regions

Блок предназначен для работы деревом регионов.

#Подключение

##Шаблоны

```
common.tmpl
```

##css

```
<link rel="stylesheet" href="/spinner/spinner.css" />
<link rel="stylesheet" href="/show-regions/show-regions.css" />
```

##js

```
<script src="/js/jquery.autocomplete.js"></script>
<script src="/js/jquery.deepcheckbox.js"></script>
<script src="/js/jquery.scrollTo.min.js"></script>
<script src="/js/utils.js?v=3"></script>
<script src="/spinner/spinner.js"></script>
<script src="/show-regions/show-regions.js"></script>
```

не забываем про jQuery

```
<script src="//yandex.st/jquery/1.8.2/jquery.min.js"></script>
```


#Макросы

`show_region_modal(target)` - строит модальное окно, вызывается один раз на странице  

* `target` - id модального окна(по умолчанию `setRegionsModal`)


`show_region_button(params)` - строит кнопку «Уточнить», скрытый инпут, читаемую строку, можно передать

* `params.name` - name скрытого инпута
* `params.value` - строка id-регионов
* `params.target` - id открывающегося модального окна(по умолчанию `setRegionsModal`)
* `params.readable` - читаемая строка выбранных регионов
* `params.text` - текст кнопки (по умолчанию «Уточнить»)

#Пример

Одно модальное окно, сколько угодно кнопок

```
[% show_region_modal(); %]
[% show_region_button({ name = 'asdasd', value = '225,1,-213,73,-11398,-11403,-11409,-11457,-10251,-11450,977' }); %]
[% show_region_button({ name = 'asdsadsa', value = '115,117,125,149,159,167,168,170,171,187,206,207,208,209,225,977' }); %]
```

Можно для каждой кнопки создавать свое модальное окно

```
[% show_region_modal('modal1'); %]
[% show_region_button({ name = 'asdasd', target = 'name1', value = '225,1,-213,73,-11398,-11403,-11409,-11457,-10251,-11450,977' }); %]

[% show_region_modal('modal2'); %]
[% show_region_button({ name = 'asdsadsa', target = 'name2', value = '115,117,125,149,159,167,168,170,171,187,206,207,208,209,225,977' }); %]
```
