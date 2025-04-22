## FAQ
<details>
<summary>Как добавить задачу в хобо</summary>

1. Простой путь:
    * Перейти в раздел создания задачи: https://hobo.test.vertis.yandex-team.ru/create
        * Выбрать очередь
        * Нажать "Взять пример" - пэйлоад предзаполнится содержимым задачи из этой же очереди (при её наличии)
        * Нажать "Создать"
2. Сложный путь:
    * Получить в [hobo-api/swagger](http://hobo-api.vrts-slb.test.vertis.yandex.net/swagger/) задачу `GET /queue/{queue}/task` (не забудьте выбрать нужную очередь).
    * Найти там `payload`, например:
   ```json
       "payload": {
          "type": "external",
          "ids": [
            "CARS:1090498536-66349935"
          ]
        },
   ```
* Отправить этот `payload` в ручку создания таски `POST /queue/{queue}/task`, например:
  ```curl
  POST /api/1.x/queue/AUTO_RU_COMPLAINTS_VISUAL/task HTTP/1.1
  Content-Type: application/json
  {
    "payload": {
    "type": "external",
    "ids": [
      "CARS:1089444464-8124b162"
    ]
    }
  }
  ```
</details>

<details>
<summary>ENOTFOUND - не резолвится локально хост *.query.consul</summary>
https://wiki.yandex-team.ru/users/goodfella/consul-dns-na-rabochejj-mashine/ - тут bash-скрпит, его нужно сохранить к себе и выполнить от имени sudo.
</details> 


