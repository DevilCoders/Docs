### Докеризированный tvmtool

- Сам `tvmtool` приезжает из пакета `yandex-passport-tvmtool`.
- Конфигурация лежит [здесь](./deploy/etc/tvmtool/tvmtool.conf).
- По-умолчанию `tvmtool` запускается в тестовом режиме (`--unittest`) c захордкоженным auth-токеном (см. --auth в [Dockerfile](./Dockerfile)). Этот токен нужно передавать ему в хедере Authorization во всех запросах кроме пинга.
- Флажок `--dangerous-bind-all-interfaces` нужен чтобы `tvmtool` слушал не только `localhost`. Без этого запросы из внешней сети, в частности из других контейнеров, не будут доходить до `tvmtool`. 
 