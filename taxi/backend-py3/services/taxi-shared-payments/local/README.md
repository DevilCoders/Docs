# Утилиты для локальной разработки
* `get-uid` - по account_id из таблицы accounts, получается список yandex_uid, котырй нужен для авторизации
* `psql` - стучится в тестинг по локальному secdist`у
* `run-web` - запуск сервера без tvm, перед этим нужно всё спроксировать в тестинг (паспорт, базы) - https://github.yandex-team.ru/ilchistyakov/home/tree/master/bin tvmtunnel и mtunnel
* `run-cron` - запуск крон-таски, так же нужно проксирование, попробуй команду `-h`, пример `run-cron taxi_shared_payments.crontasks.order_reports --debug`
