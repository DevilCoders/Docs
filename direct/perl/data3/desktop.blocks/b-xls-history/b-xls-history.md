r103821
#b-xls-history#

##Описание##
Вкладка "История" на странице "Управление кампаниями через xls"

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[kabzon](https://staff.yandex-team.ru/kabzon)

###Где используется###

* `p-xls-management` - как контент вкладки истории импорта/экспорта кампаний на странице управления кампаниями с помощью XLS/XLSX   

##Roadmap & known issues##

* перенести параметр `tab` в какой нить список параметров для ссылок по типу этих ссылок (сейчас используется для ссылок удаление)
* убрать параметр `login` и использовать константы
* унести `transformData` в кастомные моды

##Пример##

```

    {
        block: 'b-xls-history',
        tab: 'history',
        login: this.data.user_login,
        exported: this.data.exported_xls_list || [],
        imported: this.data.imported_xls_list || [],
        allow: {
            download: true,
            remove: !hasLoginRights('superreader_control')
        }
    }
```
