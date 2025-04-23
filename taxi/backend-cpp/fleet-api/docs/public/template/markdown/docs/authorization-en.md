# Authorization

To authorize requests:

* Partner ID **park_id**
* Client ID **X-Client-ID**
* Secret API Key **X-API-Key**

In order to get them select the "Settings" section in the Control room and proceed to the API section. Only an employee with the "Director" role can edit it.

## Request example

```bash
curl -X POST \
  https://fleet-api.taxi.yandex.net/v1/parks/driver-profiles/list \
  -H 'X-Client-ID: <Client ID>' \
  -H 'X-Api-Key: <Secret Api Key>' \
  -d '{
	"query": {
		"park": {
			"id": "<Partner ID>"
		}
	}
}'
```


## Feedback

Ask questions about authorization in the API at [api-taxi@yandex-team.ru](mailto:api-taxi@yandex-team.ru).
