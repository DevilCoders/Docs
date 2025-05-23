### Дежурства в Лего

В любой момент времени в команде Лего есть дежурный. Это ответственный разработчик, который решает вопросы:
- поддержки пользователей
- поддержки инфраструктуры Лего
- внедрения релизов Лего в сервисы.

Кроме этого, дежурный работает над задачами по уменьшению технического долга, улучшения внутренних инструментов и инфраструктуры Лего. Такие задачи в Трекере помечаются специальным тегом [`lego-duty`](https://st.yandex-team.ru/lego/order:updated:false/filter?tags=lego-duty), а их планирование и приоритизация происходит на общем планировании спринта с участием всей команды.

#### Поддержка пользователей

Дежурный помогает командам других сервисов использовать решения и технологии Лего когда они обращаются в наши каналы поддержки:
- письма в рассылку [lego@](mailto:lego@yandex-team.ru), время реакции дежурного — 24 часа
- обращения в канал [#support](https://lego-team.slack.com/messages/C0DL13NJY) в [Slack](lego-team.slack.com), время реакции дежурного — 2 часа.

Что делает дежурный:
- разбирает накопившиеся вопросы и предлагает обходные пути для исправления проблем, не дожидаясь планового релиза
- формулирует релевантную задачу в Трекере, если для решения задачи требуются усилия значение которых соответствует или превышает 1 SP
- убеждается, что пользователю понятен ответ и разъяснения.

В [Slack](lego-team.slack.com) общение с пользователями ведется в тредах. Для удобства пользователей важно маркировать два статуса обращений — анализ вопроса и его решение — любым подходящим emoji.

#### Поддержка инфраструктуры Лего

Дежурный следит за тем, чтобы автотесты в `dev` репозиториев Лего проходили успешно. Если `dev` сломан, дежурный разбирается в причине падения и формулирует задачу на разработчика Лего, из-за действий которого сборка оказалась сломана. В этом случае в Трекере заводится отдельная задача с приоритетом [`Блокер`](https://st.yandex-team.ru/lego/order:updated:false/filter?priority=blocker), которая сразу попадает в работу.

Также, дежурный проверяет [дашборд дежурного](https://st.yandex-team.ru/dashboard/14562) на наличие MQ-инцидентов в islands (раздел "Неразобранное"). Если пулл-реквест не может быть влит из-за падения одной из проверок в merge-queue, на дежурного автоматически заводится MQ-задача. Требуется самостоятельно исправить проблему и повторно поставить пулл-реквест в очередь, закрыв задачу с соответствующей резолюцией, или передать задачу в дежурных инфраструктуры, если проблема в инфраструктуре. Самостоятельно можно отключить плавающий тест или идентифицировать интеграционное падение (когда на результат теста повлиял код пулл-реквеста, влитого перед нашим). Обязательно перед работой с MQ задачами нужно прочитать [Инструкцию по разбору] (https://wiki.yandex-team.ru/search-interfaces/infra/infraspeed/process/support/duty/mq-incidents/#kakrazbiratincidenty).


#### Внедрение релизов Лего в сервисы
Дежурный помогает релиз-инженеру Лего внедрять релизы в сервисы — решает вопросы исправления автотестов в интеграционных PR's.
