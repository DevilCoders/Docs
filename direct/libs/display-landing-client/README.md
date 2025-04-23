# display-landing-client - клиент к сервису Дисплея с информацией о турбо-страницах
### основные функции
getSubmission - Получает из Конструктора информацию о заявках, оставленных клиентами на лендингах/турбо-страницах

### владелец
Команда API Директа

### hostname запроса
https://dev-turbofeedback.common.yandex.ru/direct/submissions

### пример запроса
curl --request POST \
  --url https://dev-turbofeedback.common.yandex.ru/direct/submissions \
  --header 'authorization: 59bbc2f971730e67a59be0d5' \
  --header 'content-type: application/json' \
  --cookie i=uikjk6KVDixsTcr%2BGlcjgOuj7HHrmElsoP0sSG8ZzrD4KHLi%2FLLgsP5wV6vq5PVfoxi2r5xZ%2BNwHE8grNL3xa5RBOgY%3D \
  --data '{"SelectionCriteria":{"TurboPageIds":[1000001],"ClientId":16948833},"Page":{"Limit":10001,"Offset":0}}
'

### пример ответа
```{
	"Submissions": [
		{
			"Data": [
				{
					"FieldName": "comment",
					"Value": "каменты жгут!"
				},
				{
					"FieldName": "phone",
					"Value": "+79096554329"
				},
				{
					"FieldName": "when",
					"Value": "никогда!!!"
				},
				{
					"FieldName": "fio",
					"Value": "Юрец"
				}
			],
			"Id": "5a1c0c047090c7002cdb4798",
			"SubmittedAt": "2017-11-27T12:58:44+00:00",
			"TurboPageId": 1000001,
			"TurboPageName": "New Turbo page"
		},
		{
			"Data": [
				{
					"FieldName": "comment",
					"Value": "11"
				},
				{
					"FieldName": "phone",
					"Value": "11"
				},
				{
					"FieldName": "when",
					"Value": "11"
				},
				{
					"FieldName": "fio",
					"Value": "Konstantin"
				}
			],
			"Id": "5a1c0ca07090c7003081b56c",
			"SubmittedAt": "2017-11-27T13:01:20+00:00",
			"TurboPageId": 1000001,
			"TurboPageName": "New Turbo page"
		}
	]
}
```

