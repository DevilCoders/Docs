# Описание логов UserJournal

## Получение письма

    {
         "affected" : "1",
         "ip" : "199.16.156.162",
         "date" : 1487072426606,
         "state" : "161285161655215669",
         "mid" : "161285161655215669",
         "target" : "message",
         "filterIds" : "384185,1312312",
         "fid" : "2",
         "operation" : "receive",
         "ftype" : "4",
         "emailFrom" : "info@twitter.com",
         "module" : "fastsrv",
         "connectionId" : "MnEgcxj7DR-eCi8tZSV",
         "subject" : "Mail Subject",
         "msgId" : "<64.C6.46946.C9CE2A85@twitter.com>",
         "unixtime" : "1487072426",
         "suid" : "3547214696",
         "labelSymbols" : ",,,,recent_label,spam_label",
         "hidden" : "0",
         "stid" : "105811.354723696.428299074341822385330916276684",
         "mdb" : "pg"
    }
    
    
Поля:

* module - **fastsrv**
* ftype - тип папки:
     * 0 пользовательские
     * 1 входящие
     * 2 отправленные
     * 3 удаленные
     * 4 спам
     * 5 черновики
     * 6 исходящие (в случае отложенной отправки или повторной попытки отправки, которую использует некоторые клиенты. например, imap
     * 7 архив
     * 8 шаблоны
* mid - глобальный идентификатор письма     
* fid - идентификатор папки
* operation - тип операции:
    * receive - получение письма
* emailFrom - email отправителя
* unixtime - timestamp получения письма
* hidden - письмо скрыто (в случае создание черновика)
* filterIds - список фильтров, которые были применены к письму
* labelSymbols - метки письма, разделены запятой (см. [описание](https://wiki.yandex-team.ru/sergejjxandrikov/novoemetaxranilishhe/metki/#simvolymetok))


## Операции с письмами

      {
         "affected" : "1",
         "ip" : "2a02:6b8:0:40c:bdb8:e4c0:cfd1:7523",
         "date" : 1487077631551,
         "mids" : "161285161655215666",
         "userAgent" : "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/602.2.14 (KHTML, like Gecko) Version/10.0.1 Safari/602.2.14",
         "test-buckets" : "36569,0,7;36596,0,12;25469,0,23;34680,0,61;37979,0,36",
         "state" : "read;161285161655215666",
         "target" : "message",
         "msgStatus" : "read",
         "enabled-test-buckets" : "36569,0,7;36596,0,12;25469,0,23;34680,0,61;37979,0,36",
         "operation" : "mark",
         "module" : "mailbox_oper",
         "requestId" : "9d578ffcded0c6c17377d80bfcb8c791",
         "connectionId" : "u2709-1487077604129-18939918",
         "clientVersion" : "12.9.300",
         "clientType" : "LIZA",
         "unixtime" : "1487077631",
         "suid" : "354723696",
         "mdb" : "xdb46"
      }
     
Поля:

* module - **mailbox_oper**
* operation - операция над письмом:
    * spam – пометили спамом
    * unspam – убрать из спама
    * purge – удалить письмо насовсем
    * trash – переместить в корзину
    * mark – пометить письмо (см. поле msgStatus)
    * move - перемещение письма (cм. destFid)
    * label - поставить пользовательскую метку
    * unlabel - снять метку
    * delete_folder - удалить папку
    * delete_label - удалить метку совсем
* msgStatus - статус письма:
    * read - прочитано
    * not_read - не прочитано
    * replied - ответили
    * forwarded – форваднули
* mids - идентификаторы писем
* destFid - в случае операции `move` идентификатор папки, куда перемещаются письма
* unixtime - timestamp операции


## Операции IMAP

    {
         "affected" : "1",
         "ip" : "::ffff:5.45.212.69",
         "date" : 1486565541498,
         "unixtime" : "1486565541",
         "state" : "8184",
         "target" : "message",
         "suid" : "1120000000136051",
         "operation" : "imap_flags",
         "mdb" : "mdb100",
         "module" : "yserver_imap"
      }
      
Поля:

* module - **yserver_imap**
* operation - операция:
    * authorization - авторизация
    * move - переместить в папку
    * abuse - помечено спамом
    * create - создание папки
    * delete - удалить папку
    * clear - отчистить пользовательские метки
    * rename - переименовать папку
    * append - операция вставки сообщения IMAP
    * reset_fresh - обновление счетчика свежести
    * imap_flags - поставить метки IMAP
    * imap_purge - удалить письмо насовсем
* mids - идентификаторы писем
* unixtime - timestamp операции
