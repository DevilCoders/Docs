# Цель RFC
Согласовать формат ссылки на QR кодах

# Процесс
Пользователь сканирует внешней камерой QR с урлом (см ниже):
* если приложение установлено, то из камеры можно сразу попасть в него, где мы покажем пречек с возможностью оплаты
* если не установлено, то откроется браузер с ссылкой из QR. Там пользователь узнает, что от него хотели и сможет перейти и скачать приложение

# Предложение
1. Зафиксировать формат ссылки: 
`https://taxi.yandex.ru/action/qr?id=<id>&hmac=<hmac>`

2. Загрузить json файл вида 
```json
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "WSFTBG7L56.ru.yandex.taxi.develop",
        "paths": [
          "/action/qr/*"
        ]
      },
      {
        "appID": "PGB36VEQ8D.ru.yandex.taxi",
        "paths": [
          "/action/qr/*"
        ]
      }
    ]
  }
}
```
так чтобы он был доступен без редиректов по `https://taxi.yandex.ru/.well-known/apple-app-site-association`

В андройде - сделать по инструкции: https://developer.android.com/studio/write/app-link-indexing#associatesite


3. Сделать по адресу лендинг, чтобы переход по https://taxi.yandex.ru/action/qr?id=<id>&hmac=<hmac> открывался в браузере.
