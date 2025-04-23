### Отправить документ на индексацию:
- TVM токен из секретницы кладем в DATACAMP_TVP_SECRET:
```bash
export DATACAMP_TVM_SECRET=xxx
можно так:
export DATACAMP_TVM_SECRET=`ya vault get version sec-01dsfcej668h548vxvxgh8vw41 -o tvm-token-datacamp-white-testing`
```
- Запустить saas_client в режиме Indexer:
```bash
./bin/saas_client -c conf/market_datacamp_test_blue --document-offer-id bestTVEver --document-shop-id 10265867 --document-warehouse-id 171 --mode Indexer
./bin/saas_client -c conf/market_datacamp_prestable --mode Indexer --document-united --document-filename offer.json
```
- Проверить, что документ проиндексирован (процесс может занять несколько минут):
```bash
curl -s 'http://saas-searchproxy-prestable.yandex.net:17000/market_datacamp_test?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_offer_id:"bestTVEver"&hr=json&numdoc=10&p=0' | jq .
```
- При отсутствии оффера можно посмотреть на ошибки индексации в [админке сервиса](https://saas-mon.n.yandex-team.ru/export_errors?ctype=prestable&service=market_datacamp_test)
- Если совсем грустно, можно сходить в чатик saas-duty или создать тикет в SAASSUP

### Как сходить в продовый саас с tvm
1. Создать токен (режим GenTvmTicket):
```bash
./bin/saas_client -c "conf/market_datacamp_shop" --saas-tvm-secret "xxx" --mode GenTvmTicket
```

2. Сохранить значение в TVM_TICKET:
```bash
export TVM_TICKET=3:serv:xxx
```

3. Выполнить запрос:
```bash
 curl -sH "X-Ya-Service-Ticket: ${TVM_TICKET}" 'http://saas-searchproxy.yandex.net:17000/market_datacamp_shop?ms=proto&kps=574823&text=s_offer_id:"0-03-804"&gta=offer_id&hr=json' | jq .
```

### Удалить документ из saas
- TVM токен из секретницы кладем в DATACAMP_TVP_SECRET:
```bash
export DATACAMP_TVM_SECRET=xxx
```
- Запустить saas_client в режиме Deleter:
```bash
./bin/saas_client -c conf/market_datacamp_stable --document-offer-id 5497 --document-business-id 1016426 --mode Deleter
```
