###Перемодерация объявлений для Наружной рекламы в попапе групп

####Запросы в базу чтобы менять статусы модерации
```
direct-sql ts:ppc:9 'select * from moderate_banner_pages where bid = 7776263173'
direct-sql ts:ppc:all "UPDATE  moderate_banner_pages SET statusModerate='No' WHERE moderate_banner_page_id=423"
```

```
direct-sql dt:ppc:5 'select * from moderate_banner_pages where bid = 7100327026'
direct-sql dt:ppc:5 'update moderate_banner_pages set statusModerate = "Yes" where moderate_banner_page_id = 1000000014'
```

###Автор
[lento4ka](https://staff.yandex-team.ru/lento4ka)
