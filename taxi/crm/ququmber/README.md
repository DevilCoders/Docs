Про сервис
https://wiki.yandex-team.ru/taxi/backend/architecture/ququmber/

Про java framework https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/

## Генерация проекта IDEA

Выполнить:

```bash
~/arcadia/taxi/crm/ququmber/generate_project.sh -i /Users/$USER/projects/
```

После этого в папке projects создастся папка ququmber c проектом IDEA и "Run Service (generated)" конфигурацией

## Запуск локально:

В конфигурацию запуска в IDEA добавить системную переменную YAV_AUTH_TOKEN со значением
из https://yav.yandex-team.ru/secret/sec-01fr59ss9w6ry71nerrxwh15t2
(Тут плохо что локальная среда и прод среда работает под одним и тем же роботом robot-ququmber. Надо завести под
local+testing и prestable+stable отдельных роботов с разными доступами)

Потом запускать из IDEA

# Трекер

Общался с @rostovsky @lyle @ekks-job Приложение https://oauth.yandex.ru/client/a4c9aed0917a40b0965fb93482df3174
Логин robotququmber@yandex-taxi.yaconnect.com

Токен надо обновлять руками в секретнице раз в год! Ничего себе

# saas_push

https://wiki.yandex-team.ru/jandekspoisk/saas/datadelivery/pq/demon-dlja-zapisi-v-saas-cherez-lb/#konfig
Чтобы запускать локально на macos, надо взять бинарник демона у коллеги или собрать самостоятельно:

```bash
cd ~/arcadia/saas/tools/saas_push && \
ya make -r -o=/tmp && \
mv /tmp/saas/tools/saas_push/saas_push ~/bin/
```

TVM_SECRET брать из https://yav.yandex-team.ru/secret/sec-01fqnzck1zmb0segge7kzz0p3d

```bash
export TVM_SECRET=??? && \
export TVM_ID=2032492 && \
~/bin/saas_push -c /Users/turkin/arcadia/taxi/crm/ququmber/deploy/saas_push/saas_push.testing.conf
```

# Переиндексация
Пробегает по всем заказам чекаутера во временном интервале.
Запускать на прод хосте, дернув http ручку (см ниже).
Состояние переиндексации хранится в файле ${reindex.workdir}/reindex (на проде /var/log/yandex/ququmber/reindex)
Поэтому приложение можно перезапускать - реиндексация начнется с того места, где остановилась.

Код смотреть в ReindexTaskManager.

Можно дергать ручки:
curl "http://localhost:8090/reindex" - статус. Включено ли, сколько еще осталось индексировать.
curl -v -X POST -G --data-urlencode "from=2022-01-01 00:00" --data-urlencode "to=2022-06-08 00:00" "http://localhost:8090/reindex" - поставить задачу на переиндексацию
curl "http://localhost:8090/reindex/stop" - приостановить
curl "http://localhost:8090/reindex/start" - запустить
curl "http://localhost:8090/reindex/clear" - стереть интервалы для переиндексации, фактически остановка.
