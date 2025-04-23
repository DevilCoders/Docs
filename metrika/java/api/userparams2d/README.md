# USERPARAMS2D
Обработчик параметров посетителей

## Описание
Читает пошардированный топик, в который пишет `userparams-sharder` и приходят загрузки из ручек `UserParamsController` в `faced`, смотрит есть ли изменения среди пришедших параметров посетителей и в случае их наличия обновляет таблицы в YT и пишет соответствующие параметры в `userparams-giga-log` и `userparams-nano-log`. От туда их потом забирает дата трансфер и пишет в КХ. Также во время обработки демон привязывает `client_user_id` к `user_id`.



### Читает:
топик `userparams-sharded-log`

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-sharded-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1641743436448&metricsTo=1641829836450&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-sharded-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1638975593906&metricsTo=1639061993907&sortOrder=%22default%22)

консьюмер `userparams-updates-consumer`

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-updates-consumer?page=statistics&type=consumer&tab=readMetrics&metricsFrom=1641746147401&metricsTo=1641832547402&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-updates-consumer?page=statistics&type=consumer&tab=readMetrics&metricsFrom=1641746124988&metricsTo=1641832524988&sortOrder=%22default%22)

[формат protobuf](https://a.yandex-team.ru/arc_vcs/metrika/java/api/management-common/proto/userparams.proto)
### Пишет:

* В первую очередь демон пишет в дин таблицы на YT. По этим таблицам обновляется версия и проверяется, что параметр обновился. Также по этим таблица производится маппинг `user_id` и `client_user_id` при обработке оффлайн конверсий.

    Таким образом предполагается что эти таблицы - нерушимый столп поддерживающий параметры посетителей и содержащий наиболее достоверную информацию о них. В случае каких либо протечек данных из CH (например из-за дататрансфера или потере данных по ttl в nano/giga-log топиках) восстановление предполагается именно из этих таблиц.

    Стоит отметить что входной топик `userparams-sharded-log` пошардирован по CHIntHash64(userId). Первым столбцом в ключе таблиц является тот же самый хэш от userId, таким образом поды максимально разнесены по партициям.

[тестинг](https://yt.yandex-team.ru/markov/navigation?path=//home/metrika/testing/userparams2)

[прод](https://yt.yandex-team.ru/markov/navigation?path=//home/metrika/userparams2)

* топик `userparams-giga-log`
В него пишутся все параметры.

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-giga-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1641746176188&metricsTo=1641832576188&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-giga-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1641746190980&metricsTo=1641832590981&sortOrder=%22default%22)

* топик `userparams-nano-log`
В него пишутся лишь параметры, принадлежащие "небольшим" счетчикам. Для определения большой счетчик или нет используется `BignessSerivce`.

[тестинг](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/test/userparams/userparams-nano-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1641746357810&metricsTo=1641832757810&sortOrder=%22default%22)

[прод](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/userparams/userparams-nano-log?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1641746342277&metricsTo=1641832742277&sortOrder=%22default%22)


### Графики

[тестинг](https://solomon.yandex-team.ru/?project=metrika&cluster=userparams2&service=userparams2&l.env=testing)

[прод](https://solomon.yandex-team.ru/?project=metrika&cluster=userparams2&service=userparams2&l.env=production)

