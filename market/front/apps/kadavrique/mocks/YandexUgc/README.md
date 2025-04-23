# YandexUgc / SerpUGC

## Опросы для отзывов

По умолчанию отдает отстувие опросов. Чтобы пользователю пришел опрос, его надо задать в схеме.

Пример схемы `schema.reviewPoll`:
```
{
	"reviewPoll": {
		"100500": { // userId
			"token": "ABC",
			"record": {
			    "type": "shop",
			    "shop": {
			        "id": "123",
			    }
			}
		}
	}
}
```
