---
title: Эксплуатация
rank: 30
---
### Эксплуатация

- [Проект в Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/travel/notifier)

### Хранилище
#### `PostgreSQL`
- [testing](https://yc.yandex-team.ru/folders/foo1262pmfvsq72flh90/managed-postgresql/cluster/mdb9sssbmtcje8gtvlrc?section=databases)
- `TODO: ссылка на прод yc`

### Деплой
- [Релизный граф](https://a.yandex-team.ru/arc/trunk/arcadia/travel/notifier/a.yaml)
- [Релизы в NewCI](https://arcanum.yandex-team.ru/ci/ticket/releases/timeline?dir=travel%2Fnotifier&id=travel-notifier-release)
- [Проект в Y.Deploy](https://deploy.yandex-team.ru/projects/travel-notifier)

**Требования к метрикам**

Кроме базовых метрик grpc сервиса `тут ссылка` собираются:

  - количество отправленных уведомлений по типам
  - количество неотправленных уведомлений по типам
