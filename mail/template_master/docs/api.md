## /force_detemple

Производит поиск шаблона для письма среди шаблонов находящихся в памяти инстанса, т.е внутри template pool'a


    curl 'template-master.mail.yandex.net:443/force_detemple' -d @data.json
<details><summary><b>data.json</b></summary><p>

```json
{
"stid": "123",
"subject": "123", 
"from": "123", 
"queueId": "123", 
"html": "\r\n<html><body><p>Уважаемые покупатели!</p>\r\n<p>Обращаем Ваше внимание, что сегодня в продажу на сайте поступили новые <strong>монеты Великобритании, Канады и Каталог-справочник монет РСФСР, СССР и России 1921-2020 \"Конрос\" август 2019!</strong></p>\r\n<p>В случае, если монету из списка нельзя добавить в корзину, это значит, что она уже куплена.</p><hr />\r\n<div>\r\n<p>Интернет-магазин ZooCoin</p>\r\n<p><a href=\"http://zoocoin.ru\">http://zoocoin.ru</a></p>\r\n</div></body></html>\r\n"
}
```
</p></details>
<details><summary><b>Response</b></summary><p>

```json
{
 "status": "FoundPreparedInPool",
 "delta": [[],
  ["<br />", "<br />"],
  ["С Уважением!"],
  ["Управление по текущему ремонту дорог"],
  ["ГБУ \"Автомобильные дороги\""],
  []],
  "attributes": [
    {"from": "noreply@auto.ru",
     "subject": "111",
     "queue_id": "123"},
    {"from": "noreply@auto.ru",
     "subject": "333",
     "queue_id": "444"},
    {"from": "noreply@auto.ru",
     "subject": "Новые объявления: Land Rover  Rover IV",
     "queue_id": "5555"},
    {"from": "noreply@auto.ru\n",
     "subject": "Новые объявления:  Solaris",
     "queue_id": ",<HVIfvGkFpB-DEbSmXbw> "}
   ],
  "stable_sign": 34556122178105241
 }
```
</p></details>

## /detemple
Производит поиск шаблона для письма в БД, если шаблон найден возращает ответ, если не найден, то выбирает инстанс 
template master'a и пересылает запрос туда в ручку **/force_detemple**
    
    curl 'template-master.mail.yandex.net:443/detemple' -d @data.json
<details><summary><b>data.json</b></summary><p>

```json
{
"stid": "123",
"subject": "123", 
"from": "123", 
"queueId": "123", 
"html": "\r\n<html><body><p>Уважаемые покупатели!</p>\r\n<p>Обращаем Ваше внимание, что сегодня в продажу на сайте поступили новые <strong>монеты Великобритании, Канады и Каталог-справочник монет РСФСР, СССР и России 1921-2020 \"Конрос\" август 2019!</strong></p>\r\n<p>В случае, если монету из списка нельзя добавить в корзину, это значит, что она уже куплена.</p><hr />\r\n<div>\r\n<p>Интернет-магазин ZooCoin</p>\r\n<p><a href=\"http://zoocoin.ru\">http://zoocoin.ru</a></p>\r\n</div></body></html>\r\n"
}
```
</p></details>
<details><summary><b>Response</b></summary><p>

```json
{
 "status": "FoundInDb",
 "delta": [[],
  [", 1 новое объявление "],
  ["<a href=\"https://auto.ru/go2listing/?sort_offers=cr_date-DESC&amp;currency=RUR&amp;custom_state_key=CLEARED&amp;dealer_org_type=1&amp;dealer_org_type=2&amp;dealer_org_type=4&amp;engine_type=DIESEL&amp;gear_type=ALL_WHEEL_DRIVE&amp;geo_radius=1000&amp;image=true&amp;in_stock=false&amp;mark-model-nameplate=MITSUBISHI%23PAJERO_SPORT%23%232308045&amp;price_to=600000&amp;rid=11114&amp;state=NEW&amp;state=USED&amp;steering_wheel=LEFT&amp;transmission_full=MECHANICAL&amp;utm_source=email_newoffers&amp;utm_medium=email&amp;utm_content=listing-view-top\">",
   "Mitsubishi Pajero Sport I Рестайлинг"]],
 "stable_sign": 413409560178249439
 }
```
</p></details>

## /find_template
Производит поиск шаблона в БД по **stable sign**

    curl 'template-master.mail.yandex.net/find_template?stable_sign=714631713584594356'
<details><summary><b>Response</b></summary><p>

```json
{
"status":"Found",
"chunks":[["Уважаемый пользователь!","<br />","\r\n","<br />"],["<br />","\r\n","<br />","\r\nПроблем с дисками в DSM не обнаружено.","<br />","<br />","\r\n","<br />","\r\nС уважением,","<br />"]],
"stable_sign":656296890894902346
}
```
</p></details>
