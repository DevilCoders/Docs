#b-banner-storage-frame#

##Описание##
iframe с конструктором креативов в модальном окне.

Блок генерирует событие 'select', в которое передается массив выбранных креативов.

###Автор### 
[dima117a](https://staff.yandex-team.ru/dima117a )

##Пример##

```
    var modal = BEM.DOM.blocks['b-banner-storage-frame'].create();
    
    modal.on('select', function(e, creatives) {
        ...    
    });
    
    // открыть вкладку с галереей креативов
    modal.show('creatives', clientId, validationRules);
    
    // открыть вкладку создания креативов по шаблону
    modal.show('presets', clientId, validationRules);

```
