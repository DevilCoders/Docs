# Как руками обновить пачку офферов
NB: партнерские данные редактировать плохо :)
> Допустим нам надо, чтобы оффера прошли через контроллеры. Для активных офферов можно
> подождать обновления офферов либо их майнинга. В случае выключенных партнеров придется
> руками пофорсить их запись.

1. Достаем список идентификаторов, [например](https://yql.yandex-team.ru/Operations/YHXWQb94hnvrCMGT7JlS-su0vIi31fBbyBJabP3mhaw=)
2. Скачиваем таблицу в json формате и сохраняем в identifiers
3. В request_data.json пишем
```json
{
    "entries": [
        {
            "method": "POST",
            "business_id": (.business_id),
            "offer_id": (.shop_sku|tostring),
            "shop_id": (.shop_id),
            "offer": {
                // тут описываем united_offer 
            }
        }
    ]
}
```
4. Получаем TVM ticket и запускаем апдейт 
```bash   
export TVM_TICKET=`cat token | ya tool tvmknife get_service_ticket client_credentials -d {tvm хранилища} -s {ваш tvm}`

cat identifiers| while read row; do echo "Processing $row"; echo $row | jq -r "`cat request_data.json`" | curl -s -XPOST --header "Content-Type: application/json" --header "X-Ya-Service-Ticket: ${TVM_TICKET}" "http://datacamp.white.vs.market.yandex.net/v1/offers/united/batch?format=json" --data-binary @- > /dev/null; done
```

{% include [Delete offers](../market/idx/datacamp/dev/delete_offers/README.md) %}
