#b-href-control#

##Описание##
Блок ввода ссылки. Содержит выпадающий список выбора протокола и
поле ввода для адреса. При изменении ссылки происходит валидация:
- длина ссылки не превышает максимальную
- ссылка имеет правильный формат
- ajax-запрос на сервер для проверки, что ссылка открывается

###Автор###
[dima117a](https://staff.yandex-team.ru/dima117a )

###Где используется###
- b-href-popup
- b-banner-href

##Пример##

- вставляем блок в шаблон

```
    { block: 'b-href-control' }

```

- подписываемся на событие
```
this.findBlockInside('b-href-control').on('state:changed', function(event, data) {

    // если валидация пройдена
    if (data.isReady) {

        // получаем введенное значение
        var value = this.val();
        // value.protocol - протокол ссылки
        // value.href - ссылка без протокола
        // value.href_domain - домен от ссылки
        // value.url - полная ссылка

        ...
    }

    validatedData = data.validatedData - данные от сервера после валидации
    //validatedData.domain_sign - md5-хэш домена,
    //validatedData.domain_redir домен-редирект (если домен содержит редирект, тот домен, на который идёт редирект (или если редиректа, тот тот-же domain)),
    //validatedData.domain_redir_sign - md5-хэш редиректа,
    //validatedData.market_rating - рейтинг на маркете

    alerts = data.alerts - массив предупреждений от блока (Проверка ссылки, ошибка 404 и т.п.)
});
```
