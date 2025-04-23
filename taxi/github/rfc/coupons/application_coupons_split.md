[TAXIBACKEND-24608](https://st.yandex-team.ru/TAXIBACKEND-24608) Разделить хранение купонов по приложениям

Основная задача:

Записывать brand_name в коллекцию user_coupons и далее фильтровать по этому полю в зависимости от приложения пользователя.

Для совместимости (когда для yataxi/yango должно быть условие brand_name in [brand_name, null]) используется конфиг COUPONCHECK_DEFAULT_ENABLED_MAP.

После миграции, а именно 1) копирования brand_name=null в yataxi/yango и 2) удаления brand_name=null, всю логику для совместимости следует удалить [TODO: brand_coupons_split: delete]



__Шаги:__

1. _/v1/coupons/activate_ - если купон валиден, запоминать промокод в promocodes для документа (yandex_uid, brand_name). Пример: 
```
{  
   "_id":ObjectId("5ca4c2ac378576699ba10913"),
   "yandex_uid":"466982103",
   "brand_name": "yataxi",  // "yataxi", "yauber", "yango", ...
   "version":4,
   "updated":   ISODate("2019-05-31T18:25:24.369Z"),
   "promocodes":[  
      {  
         "code":"bad5516646",
         "activated":         ISODate("2019-04-13T15:16:54.990Z"),
      },
      {  
         "code":"kids195030225451",
         "activated":         ISODate("2019-05-31T18:25:24.367Z"),
      }
   ]
}
```
Для совместимости считать (yandex_uid, null) как (yandex_uid, "yataxi") или (yandex_uid, "yango")

2. _/v1/coupons/list_ - делать дополнительную фильтрацию по brand_name.
У текущих промокодов нет указанного brand_name, поэтому при помощи COUPONCHECK_DEFAULT_ENABLED_MAP  для yandex/yango brand_name in [brand_name, null]) 

3. _/internal/activate_bulk_ - от CRM для каждого промокода ожидаем `application_name` https://st.yandex-team.ru/TAXICRM-1477.
В соответствием с `application_name` добавляем промокод в требуемое приложение.

4. _/internal/coupon_finish_ в запрос добавлено поле `application_name` для `success=false` (потому что нам нужно знать для какого бренда вернуть промокод), возвращаем промокод в документ (yandex_uid, brand_name)

5. _/internal/generate_ в запрос добавлено поле `application_name`, сохранение промокода в документ (yandex_uid, brand_name)


Словарь для сопоставление application с брендом https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/APPLICATION_MAP_BRAND?name=APPLICATION_MAP


<hr>

**Миграция с индекса (yandex_uid) на (yandex_uid, brand_name):**
1) выкатываем версию coupons, где новые записи в db.user_coupons создаются с brand_name, а fetch ищет по (yandex_uid, brand_name) или (yandex_uid, null) для yandex/yango 
2) запускаем скрипты, которые

     2.1 удаляет уникальный индекс (yandex_uid), создает уникальный составной индекс (yandex_uid, brand_name) 
     
     2.2 для документов, где не пустой список promocodes и brand_name=null, меняем на brand_name=yataxi и создает такой же документ с brand_name=yango, а документы с пустым списком promocodes удаляем
     
3) выкатываем версию coupons, где fetch ищет исключительно по (yandex_uid,brand_name)
