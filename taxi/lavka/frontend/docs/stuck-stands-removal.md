# Проблемы с удалением стендов

Если скопилось много неудаленных стендов и проблема не в Awacs.

- Нужно зайти в [Админку](https://tariff-editor.taxi.yandex-team.ru/task-processor/providers/34/jobs?job_name=BalancerReallocateAllPods&status=in_progress) в раздел `СЕРВИС > Task Processor`
- Там выбрать раздел `clowny-balancer` и в нем вкладку `Джобы`
- Ищем джобы типа `BalancerReallocateAllPods` со статусом `in_progress`
- В спеке джобы `Показать job_vars` ищем наши сервисы, например `awacs_namespace_id "grocery-frontend-standalone.lavka.tst.yandex.net"`

Если джоба от нашего сервиса, то идем в tg [taxi-rtc-support](https://t.me/joinchat/AggzAFkove-smhuNqGiH_g) и просим подтолкнуть джобу

Далее ждем, залипшие стенды удалятся в течение часа.
