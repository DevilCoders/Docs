# ID и роутинг

Чтобы gateway как единая точка приема трафика от пользователей мог без особо сложной stateful логики направлять запросы в нужные зональные/региональные итд кластера сервисов, предлагается чтобы все ID сущностей содержали в себе идентификатор кластера сервиса. Если сервис глобальный, то у него один кластер, если региональный, по числу регионов итд. В этой папке лежат файлики `ids-<installation>.yaml`, где installation это стенд нашего Облака. 

## Формат ID

Длина ID в облаке - 100 бит, преобразованная в 20-символьную строку. Первые 15 бит это prefix. Еще 85 - случайная последовательность. Далее все эти 100 бит сериализуются в 32 разрядную систему (числа + неполный алфавит).

## Заведение ID

Checkout cloud-go repo and run from `private-api/endpoint_ids` command `./add_service.sh --location <global|ru-central1|ru-central1-a> --location-type <global|region|zone> --service <name> --env <dev|hw-ci|testing|pre-prod|prod>`

## Заведение нового стенда

```bash
echo "[]" > ids-<installation>.yaml
```

После этого можно заводить ID по инструкции заведения ID
