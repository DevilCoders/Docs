# Структура
* Общие для всех микросервисов сущности лежат в /crm/agency_cabinet/common/monitoring (проект, окружения/кластеры, генераторы метрик и прочие вспомогательные вещи)
* Каждый микросервис содержит папку monitoring, где хранятся описания всех метрик, графов и дашбордов (если такие есть)
по данному сервису в различных окружениях (prod, prestable, testing)
* Обновлятор проекта агентского кабинета в SOLOMON лежит в /crm/agency_cabinet/monitoring/bin
* Объединяющие дашборды и графы (например те, которые содержат метрики из разных микросервисов) лежат в /crm/agency_cabinet/monitoring/registry
* Метрики фронтенда лежат в /crm/agency_cabinet/monitoring/registry/sensors/frontend

# Использование SOLO
* [Читаем READme](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/monitoring/solo)
* Вдохновляемся примерами из [yabs](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/solo_yabs)

# Рекомендации по добавлению метрик
* [Читаем полезный пост](https://prime.at.yandex-team.ru/120)
* При добавлении новой метрики в один из микросервисов не забываем сразу регистрировать ее в соответствующем проекте SOLO, даже если не планируется сразу добавлять ее на какой-то либо дашборд, либо вешать алерты

# Обновление конфига и бинаря unifed_agent
1. Редактируем конфиг нужного микросервиса и с помощью теста check-config убеждаемся, что конфиг валидный
2. Заливаем новую версию конфига через ya upload, e.g.:\
   `ya upload --ttl inf -T OTHER_RESOURCE ${ARCADIA_ROOT}/crm/agency_cabinet/gateway/monitoring/unified_agent_gateway_conf.yml`\
 **N.B**: в проде используем только конфиг из trunk
3. Находим последнюю версию [бинарника](https://sandbox.yandex-team.ru/resources?type=UNIFIED_AGENT_BIN&limit=20&attrs=%7B%22released%22%3A%22stable%22%7D) unifed agent
4. Обновляем соответствущие static resource'ы в box'е - указываем rbtorrent ссылку и MD5-хэш ресурса sandbox
5. По возможности не оставляем мусор в sandbox (надо убрать TTL - inf и удалить ненужный ресурс)

# TODO
* Настроить [персистентный volume](https://wiki.yandex-team.ru/support/knowledge-base/sluzhba-podderzhki-poiskovyx-servisov/runtime-cloud/rtc/stranichki-na-viki/nastrojjka-unified-agent-v-y.deploy/) для unified agent
* Автоматизировать загрузку конфига unified agent с помощью flow в CI
* Удалить текущие примеры дашбордов и графиков, сделать более разумные примеры
