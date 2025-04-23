## О компоненте
Компонент для обработки логов обращения пользователя. На текущий момент обрабатываются только пушапи логи.
Подробнее можно почитать на вики: https://wiki.yandex-team.ru/mbi/newdesign/components/mbi-log-processor/

## Локальный запуск из IDEA
##### Use classpath of module
`mbi-log-processor`

##### Main class
`ru.yandex.market.mbi.logprocessor.MbiLogProcessor`

##### VM-options
`
-Dspring.profiles.active=local
`
##### Environment variables
Путь до папки properties.d:
`
PROPERTIES_DIR=/Users/natalokshina/workspace/arc/arcadia/market/mbi/mbi-log-processor/src/main/properties.d
`
##### Before launch
Открыть в /properties.d/local/local-application.properties.
Заменить юзернейм в market.mbi-log-processor.target.yt.common_path (это путь, куда будут генерироваться динамические таблицы).
Заменить токен и юзернейм для коннекта в YT на ваши (если у вас нет прав, используете тестинговый аккаунт).

#### Large tests with docker
Для поднятия больших тестов (в директории src/large-test) необходим поднятый локально докер.
1. Установить докер
2. Залогиниться в registry Яндекса. Инструкции можно найти тут https://wiki.yandex-team.ru/qloud/docker-registry/#authorization.
   **ВАЖНО** Делайте docker login без sudo.

---
NB. Приложение использует логброкер. Однако при поднятии локально логброкер слушатель не инстанциируется.
