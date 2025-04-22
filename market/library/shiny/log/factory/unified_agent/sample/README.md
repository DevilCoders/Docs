###  Как пощупать? ###
1. Собираем **unified agent**: `ya make logbroker/unified_agent/bin`

2. Запускаем **unified agent**: `logbroker/unified_agent/bin/unified_agent -c ua_cfg.yml`. Агент стартанет на порту `12345`, будет сохранять буфер в `data/storage` и выводить логи в `stderr`

3. Запускаем **sample**: `./sample`. Должно написаться два трейса: `Hello UA` и `Bye UA`.
