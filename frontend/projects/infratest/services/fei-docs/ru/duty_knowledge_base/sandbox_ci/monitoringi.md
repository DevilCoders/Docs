# Мониторинги

## Github Token Proxy

При срабатывании алерта github-token-proxy нужно идти читать логи в [Deploy](https://deploy.yandex-team.ru/stages/github-token-proxy/logs), там же проверить состояние инстансов. Сервис проксирует запросы в Github и Arcanum с токеном из env. Нужно понять, что сгорело: сам сервис github-token-proxy в отключке (живы ли поды, достаточно ли им ресурсов), или проблема в самом Github или Arcanum. Если проблема в низлежащей инфраструктуре, узнать у [смежников](../kanaly_i_rassylki.md), в курсе ли они об этих проблемах, при необходимости завести инцидент.

## palmsync

### `<service>.palmsync.synchronize.<build_context>`

Этот мониторинг срабатывает, если время выполнения таски синхронизации тест-кейсов в различных контекстах сборки превышает допустимое значение.

Найти таски можно по фильтрам ниже, в зависимости от контекста сборки. Выделить проблемные таски из всего списка тасок можно по времени `Execution Time`, которое будет выше 20-30 минут.

* [dev](https://sandbox.yandex-team.ru/tasks?children=true&type=SANDBOX_CI_PALMSYNC_SYNCHRONIZE&limit=20&created=14_days&input_parameters=%7B%22project_build_context%22%3A%22dev%22%7D).
* [pull-request](https://sandbox.yandex-team.ru/tasks?children=true&type=SANDBOX_CI_WEB4_MANUAL_TEST_RUN&limit=20&created=14_days&input_parameters=%7B%22project_build_context%22%3A%22pull-request%22%7D)
* [release](https://sandbox.yandex-team.ru/tasks?children=true&type=SANDBOX_CI_WEB4_MANUAL_TEST_RUN&limit=20&created=14_days&input_parameters=%7B%22project_build_context%22%3A%22release%22%7D)

> 📖 Обратите внимание, что для контекста `dev` и других контекстов используются разные Sandbox-таски. Это историческое положение, которое будет решено в FEI-15507.

При срабатывании мониторинга, как правило, проблемы можно разделить на две категории:

* Замедление или проблемы на стороне смежников (Sandbox, TestPalm).
* Замедление инструментов, запускаемых в тасках (palmsync, testpalm-cli).

Определить категорию проблем можно прочитав логи таски:

1. `log1/debug.txt` — работа Sandbox-таски.
2. `log1/testpalm_cli_clone.out.txt` — клонирование проекта в TestPalm.
3. `log1/sync.out.txt` — синхронизация тест-кейсов.
4. `log/testpalm_testcases.err.txt` — проверка сломанных тест-кейсов.

В первую очередь следует проверять (2, 3, 4), так как, исторически, проблемы чаще всего возникают при общении с TestPalm API. Если там всё хорошо, то переходим к (1), а затем подробно смотрим на лог (3), анализируя его на предмет долгих операций.

После того, как определили категорию проблемы, выбираем способ реагирования:

* Смежники — идём к смежникам.
* Замедление инструментов — идём к ответственному за ABC.

