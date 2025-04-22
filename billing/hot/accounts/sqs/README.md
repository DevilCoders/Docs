## SQS
* Endpoint http://sqs.yandex.net:8771

* Дока https://wiki.yandex-team.ru/sqs/

* Авторизация в SQS делается
    * по имени учетки (в терминах SQS - `AWS_ACCESS_KEY_ID`)
    * по OAuth токену (в терминах SQS - `AWS_SESSION_TOKEN`)
    * SQS также требует третий параметр - ключ (`AWS_SECRET_ACCESS_KEY`), но в Яндексовой инсталляции он не используется.
      Надо передавать строку ```unused```

* Мы не используем TVM вместо OAuth (хотя это и возможно) т.к. его поддержка остутствует во всех стандартных либах AWS.

* Секреты передаются в приложение через переменные окружения,
  `AWS_ACCESS_KEY_ID`, `AWS_SESSION_TOKEN`, `AWS_SECRET_ACCESS_KEY`(=unused).

* Создание тасок смотреть в [README.md](billing/hot/accounts/pkg/core/tasks/README.md)


### Дев, тест, прод
* У нас есть 3 учетки: для прода, теста и дева
  ```
  newbilling_accounter
  newbilling_accounter-test
  newbilling_accounter-dev
  ```

### Роботы
* `robot-yb-hot-account` - для походов из прода
  Его секреты https://yav.yandex-team.ru/secret/sec-01exh4gv33wz9tyvcpha3na212
  Выданы права в prod учетке кроме CreateUser, ModifyPermissions
  ```
  aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions --path newbilling_accounter --subject robot-yb-hot-account@staff --permissions AlterQueue CreateQueue DeleteMessage DeleteQueue DeleteUser DescribePath ReceiveMessage SendMessage
  ```

* `robot-yb-hot-acc-tst` - для походов из теста
  Его секреты https://yav.yandex-team.ru/secret/sec-01exh4aa504wzc5w7j8tz4xhsc
  Выданы права в dev и test учетках кроме CreateUser, ModifyPermissions
  ```
  aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions --path newbilling_accounter-dev --subject robot-yb-hot-acc-tst@staff --permissions AlterQueue CreateQueue DeleteMessage DeleteQueue DeleteUser DescribePath ReceiveMessage SendMessage
  aws ya-sqs --endpoint http://sqs.yandex.net:8771 grant-permissions --path newbilling_accounter-test --subject robot-yb-hot-acc-tst@staff --permissions AlterQueue CreateQueue DeleteMessage DeleteQueue DeleteUser DescribePath ReceiveMessage SendMessage
  ```

### Конфиг
* Конфиг sqs прописан в общий конфиг и это надо переделать todo-igogor

### Локальная работа
* Локально можно прописать секреты в файл ~/.aws/credentials
  Детали здесь https://wiki.yandex-team.ru/sqs/#security
  Но можно и пользоваться переменными окружения

* В качестве `AWS_SESSION_TOKEN` локально лучше использовать личный OAuth токен. Т.к. тогда видно кто что делал.
  Как получить - https://wiki.yandex-team.ru/sqs/security/#oauth

* Права на операции в учетке были выданы в том числе на ```svc_newbillingaccountupdater@staff``` -
  это наш сервис https://abc.yandex-team.ru/services/newbillingaccountupdater/
  Личные права есть у igogor@ и lightrevan@

* todo-igogor права на все операции даны также всему сервису и в продовой учетке `newbilling_accounter`,
  что вероятно надо урезать

* Редактирование прав можно делать через cli - https://wiki.yandex-team.ru/sqs/#cli

* Я пока дебажился в дев учетке. Но это возможно не очень будет удобно, когда будет много людей.
  todo-igogor подумать про поднятие локального SQS в докере. Рецепт уже есть, сложность в миграции всех нужных очередей.

### Создание очереди
1. Создаем json файл параметров создания очереди в папке `billing/hot/accounts/sqs/queues`
    ```json
    {
        "QueueName": "example_queue",
        "Attributes": {
            "RedrivePolicy": "{\"deadLetterTargetArn\":\"yrn:ya:sqs:ru-central1:newbilling_accounter-dev:example_deadletter\",\"maxReceiveCount\":\"3\"}"
        }
    }
    ```
    * Названия атрибутов вместе с описаниями можно увидеть здесь https://docs.aws.amazon.com/cli/latest/reference/sqs/create-queue.html#options
    * Дефолтные значения для большинства атрибутов пока кажутся разумными
    * RedrivePolicy - см ниже, про deadletter очереди
    * Файлы с параметрами будут к сожалению не идентичны на деве тесте и проде,
      т.к. ARN deadletter очереди в каждой будет разный.
      Поэтому файлы надо разложить по папкам `dev`, `test`, `prod`, подменив соответственный deadletter
      todo-igogor это теоретически можно было бы автоматизировать:
      получать ARN для конкретного deadletter в конкретной учетке и проставлять его в очередь через set-queue-attributes

1. Зовем команду создания
   ```
   export AWS_SECRET_ACCESS_KEY=unused
   export AWS_SESSION_TOKEN={your_oauth_token}
   cd $ARCADIA_ROOT/billing/hot/accounts/sqs
   # dev
   AWS_ACCESS_KEY_ID=newbilling_accounter-dev aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://dev/example_queue.json
   # test
   AWS_ACCESS_KEY_ID=newbilling_accounter-test aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://test/example_queue.json
   # prod
   AWS_ACCESS_KEY_ID=newbilling_accounter aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://prod/example_queue.json
   ```
   Не забываем что если используем новую deadletter очередь, то ее надо создать первой.
   Иначе ошибка `Cannot create queue: Target DLQ does not exist`
   Но большинство очередей будут думаю смотреть в одну deadletter очередь и ее создать только в первый раз.
   ```
   export AWS_SECRET_ACCESS_KEY=unused
   export AWS_SESSION_TOKEN={your_oauth_token}
   cd $ARCADIA_ROOT/billing/hot/accounts/sqs
   # dev
   AWS_ACCESS_KEY_ID=newbilling_accounter-dev aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://dev/example_deadletter.json
   # test
   AWS_ACCESS_KEY_ID=newbilling_accounter-test aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://test/example_deadletter.json
   # prod
   AWS_ACCESS_KEY_ID=newbilling_accounter aws --endpoint http://sqs.yandex.net:8771 sqs create-queue --cli-input-json file://prod/example_deadletter.json
   ```


### Создание DeadLetter очереди
Эта очередь куда перемещаются сообщения которые не удалось обработать определенное кол-во раз (сообщение было считано, но не было удалено).
По сути является самой обычной очередью. Создается, обновляется, получаются сообщения - все как в обычной очереди.


Чтобы настроить в какой-то очереди перемещение сообщений в deadletter надо задать ей атрибут `RedrivePolicy`
В атрибут надо записать строку содержащую json с 2мя полями
* deadLetterTargetArn - содержит aws идентификатор очереди которую хотим использовать как deadletter для данной.
  Можно получить из атрибута `QueueArn` вызовом
   ```
   aws --endpoint http://sqs.yandex.net:8771 sqs get-queue-attributes --queue-url http://sqs.yandex.net:8771/newbilling_accounter-dev/example_deadletter --attribute-names All
   ```
* maxReceiveCount - если сообщение было считано maxReceiveCount раз, но так и не было удалено оно перемещается в deadletter очередь.
  Для разных очередей можно назначать разное, даже если они настроены на одну deadletter очередь.

```
aws --endpoint http://sqs.yandex.net:8771 sqs set-queue-attributes --queue-url http://sqs.yandex.net:8771/newbilling_accounter-dev/example_queue2 --attributes '{"RedrivePolicy": "{\"deadLetterTargetArn\":\"yrn:ya:sqs:ru-central1:newbilling_accounter-dev:example_deadletter\",\"maxReceiveCount\":\"6\"}"}'
```


Для самой deadletter очереди задавать атрибут `RedrivePolicy` смысла не имеет.
```json
{
    "QueueName": "example_deadletter",
    "Attributes": {
        "MessageRetentionPeriod": "1209600"
    }
}
```
MessageRetentionPeriod - сколько сообщение будет лежать в очереди, пока не будет удалено (в секундах).
Для deadletter имеет смысл задавать побольше. В данном примере максимальное значение 1209600 - 14 дней в секундах.
