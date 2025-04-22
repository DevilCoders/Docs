## Добавление Juggler-проверки

1. Опишите логику проверки в виде скрипта и обратите внимание на:
   - [shebang](https://ru.wikipedia.org/wiki/Шебанг_(Unix)) первой строчкой;
   - добавление в `MANIFEST.json`;
   - (опционально, если скрипт не на Python) добавление в `bundle.json`.
2. Удостоверьтесь, что все [требования](https://docs.yandex-team.ru/juggler/client/bundles#requirements) соблюдены;
3. Протестируйте проверку, запустив её на любом сервере;
4. Закоммитьте проверку в [sandbox/juggler](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/juggler);
5. Добавьте к ней агрегат с алертом типа [такого](https://juggler.yandex-team.ru/check_details/?host=sandbox.production.clients&service=dead&last=1DAY);
6. Подождите немного: раз в десять минут запускается [планировщик](https://sandbox.yandex-team.ru/scheduler/10517/view),
   пакующий все проверки Sandbox в тарболл, который раз в десять минут скачивает и распаковывает juggler-client.

Подробности: https://docs.yandex-team.ru/juggler/client/basics

Если что-то пошло не так, можно почитать логи:
```sh
tail -n 1000 /home/monitor/juggler/varlib/juggler-client.log
```
Или посмотреть, откуда проверки приезжают:
```sh
jclient-api print-config
```
Или запустить отдельную проверку:
```sh
jclient-api run-check --service fastbone_sandbox
```
