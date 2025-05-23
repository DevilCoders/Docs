## Образ

Образ поставляется в виде .tar файла, загрузить его можно с помощью команды
```
docker load < badoo-image-classifier.tar
```

Запуск образа:
```
docker run -p 80:80 --rm -d badoo-image-classifier:latest
```

После запуска образ будет в рабочем состоянии через несколько секунд, до этого могут наблюдаться ошибки `502 Bad Gateway`.

## API

### Запрос

Content-Type: multipart/form-data

```
curl http://127.0.0.1/v1/classify -X POST -F "data=@image.jpg" -F "model=badoo"
```

Поддерживаются только картинки формата .jpg.

### Ответ

Content-Type: application/json

```json
{
	"classes": {
		"AdultAndChild":0.000573428813368082,
		"Erotic":0.020453432574868202,
		"Female":0.9080814123153687,
		"Group":0.0014147654874250293,
		"Male":0.0007101080263964832,
		"Other":0.04368890821933746,
		"Trash":0.024228159338235855,
		"Weapon":0.0008498174720443785
	},
	"model":"badoo"
}
```

В случае некорректного запроса возвращается статус-код 400 с json ошибки:
```json
{"message": "Invalid data format"}
```

```json
{"message": "Only JPEG images are supported"}
```

### Производительность

Ниже для разных RPS указана 95 перцентиль времени ответа образа (время указано в миллисекундах):
* 8 RPS – 135ms
* 10 RPS – 150ms
* 12 RPS – 944ms
* 14 RPS – 3100ms

Опыты проводились с помощью .jpg картинки размера 38Kb и разрешения 600x400, на 16 ядрах с 64Gb оперативной памяти.

Для лучшей производительности рекомендуется посылать в API картинки небольшого размера с разрешением 299x299.
