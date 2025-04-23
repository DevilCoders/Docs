Стартрек умеет слать пуши по конктретным событиям:
https://doc.yandex-team.ru/tracker/external/user/trigger.html

Мы поднимает сервис который ждёт эти пуши, форматиирует их и постит в чатик суть.

##AUTORUAPPS

[Описание](https://www.evernote.com/shard/s50/client/snv?noteGuid=74fd850f-c847-4257-8203-215e750b546b&noteKey=60b0ecd37a0be259&sn=https%3A%2F%2Fwww.evernote.com%2Fshard%2Fs50%2Fsh%2F74fd850f-c847-4257-8203-215e750b546b%2F60b0ecd37a0be259&title=%25D0%25A1%25D0%25BE%25D0%25BE%25D0%25B1%25D1%2589%25D0%25B5%25D0%25BD%25D0%25B8%25D1%258F%2B%25D0%25B2%2B%25D1%2580%25D0%25B5%25D0%25BB%25D0%25B8%25D0%25B7%25D0%25BD%25D1%258B%25D0%25B9%2B%25D0%25BA%25D0%25B0%25D0%25BD%25D0%25B0%25D0%25BB)

Триггер:
https://st.yandex-team.ru/admin/queue/AUTORUAPPS/triggers/1772

Данные прилетают из стартрека в таком формате (явно прописано в триггере)

Автору: -1001228464997
Недвига: -1001075823990

```json
{
"chatId": "-1001228464997",
"issue": "{{issue.key}}",
"type": "{{issue.type}}",
"previousStatus": "{{issue.previousStatus}}",
"status":"{{issue.status}}",
"fixVersions": "{{issue.fixVersions}}",
"resolution": "{{issue.resolution}}",
"components": "{{issue.components}}"
}
```

Старт:

```text
cd release-issue-notifier
./mvnw clean install
nohup java -jar target/release-issue-notifier-0.0.1.jar --vertis.debug=false --vertis.robot.token=<TOKEN_FOR_ST> &
```

## Start

cd release-issue-notifier
./mvnw clean install
nohup java -jar target/release-issue-notifier-0.0.1.jar --vertis.debug=false --vertis.robot.token=<токен чтобы сходить в стартрек>> &