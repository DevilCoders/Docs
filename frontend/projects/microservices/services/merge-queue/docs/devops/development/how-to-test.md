# Как протестировать изменения

На примере проверки изменений в создании стартрек-задач о MQ-инцидентах.

## Немного магии
```bash
microservices$ echo '{"create_mq_issue": true}' > services/merge-queue/config/service-config.json
```

## Настройка туннеля
Тестировать мы будем на настоящем репозитории, поэтому нам потребуется туннель до локальной машины.
Используем свою QYP виртуаль, например: `username-dev.sas.yp-c.yandex.net`

### Разрешаем проксирование
```bash
ssh username-dev.sas.yp-c.yandex.net
sudo vim /etc/ssh/sshd_config
# находим #GatewayPorts no, убираем #, меняем no на yes
# если такой строчки нет, то просто добавляем GatewayPorts yes

# перезапускаем ssh
sudo service ssh restart
```

### Поднимаем туннель
Возвращаемся на локальную машину и в отдельной вкладке терминала запускаем:
```bash
ssh -R '[::]:9000:[::1]:3000' -N username-dev.sas.yp-c.yandex.net -v
```
Где `9000` это незанятый порт на хосте в QYP, а `3000` – порт локально запущенного MQ-сервиса.

Мы должны увидеть сообщение вида `remote forward success for: listen 9000, connect localhost:3000`.

Проверяем, что туннель работает:
```bash
curl -v http://username-dev.sas.yp-c.yandex.net:9000
```

Переходим в окно терминала, где запускали MQ-сервис, и смотрим, что получили там:
```bash
2019-01-15T13:18:47.634Z → ::1 "GET username-dev.sas.yp-c.yandex.net / - - -"
2019-01-15T13:18:47.721Z ← ::1 "GET username-dev.sas.yp-c.yandex.net / - - -" 302 117 69.345 ms
```

## Тестовый репозиторий

Существует два тестовых репозитория:
1. [MQ over Trendbox](https://github.yandex-team.ru/search-interfaces/trendbox-ci-with-mq)
2. [MQ over sandbox_ci](https://github.yandex-team.ru/search-interfaces/merge-queue-test-project)

Желательно тестировать свои изменения на обоих.

### Перенаправляем хук
Переходим на страницу настройки хуков в нужном репозитории (`Settings` -> `Hooks`).

Нас интересует `issue-comment`, меняем ему `Payload URL` на `http://username-dev.sas.yp-c.yandex.net:9000/v2/github/issue-comment`.

### Проверяем

Достаточно зайти в любой закрытый pull-request и написать там `/merge`, в окне терминала с запущенным MQ-сервисом получим:
```bash
2019-01-15T13:24:27.668Z → ::1 "POST username-dev.sas.yp-c.yandex.net /v2/github/issue-comment search-interfaces/trendbox-ci-with-mq issue_comment ddbd5750-18c8-11e9-94aa-2359aca1d458"
  merge-queue:issue-comment-handler an event happened not in an open pull request, ignoring +0ms
2019-01-15T13:24:27.692Z ← ::1 "POST username-dev.sas.yp-c.yandex.net /v2/github/issue-comment search-interfaces/trendbox-ci-with-mq issue_comment ddbd5750-18c8-11e9-94aa-2359aca1d458" 204 - 22.951 ms
```

Успех! Комментарий в репозитории был обработан нашей локальной инсталляцией.

## Эмулируем падение обязательной проверки

### Для репо `trendbox-ci-with-mq`

Отвёдем ветку в тестовом репозитории, в ней заменим код trendbox-job'ы на `sleep 2m && exit 1`:
```bash
trendbox-ci-with-mq$ git df
diff --git a/.trendbox.yml b/.trendbox.yml
index f57ed44..de3c7d0 100644
--- a/.trendbox.yml
+++ b/.trendbox.yml
@@ -6,4 +6,4 @@ language: node_js

 node_js: 8.9.4

-script: sleep 2m
+script: sleep 2m && exit 1
```

Открываем PR из нашей ветки и пишем в нём `/merge`.

### Для репо `merge-queue-test-project`

Идём в `Settings` -> `Branches` -> `Branch protection rules` -> `master`.

Отмечаем `[Sandbox CI] Красная проверка` как обязательную.

Открываем PR из нашей ветки и пишем в нём `/merge`.

### Результат

Через несколько минут получим тикет в тестовом Стартреке, [например](https://st.test.yandex-team.ru/MQ-75). Теперь можно тестировать свой патч :)

Также следует учесть, что просто подряд спамить `/merge` не выйдет, тикет создается только для падений непосредственно в MQ.
Это не всегда удобно, но нормально исправить это для тестовой среды не удалось, поэтому при желании уберите проверку в методе `send` в `services/merge-queue/modules/notifications/report-incidents.js`.

## Неочевидные детали

1. Тестовый Стартрек периодически валяется, возможно, придётся потерпеть.
2. В тестовом Стартреке нет правильной дежурной задачи, поэтому в коде сервиса пришлось проверять окружение, иначе никак.
