---
title: Локальная разработка
rank: 20
---

### Настройка окружения

Запускать нужно [ExternalApiApplication](https://a.yandex-team.ru/arc/trunk/arcadia/travel/external_api/src/main/java/ru/yandex/travel/externalapi/ExternalApiApplication.java)
Чаще всего Внешнее АПИ имеет смысл запускать локально вместе с Администратором.

Для запуска нужно настроить следующие интеграции:
1. **Отключить авторизацию**
```yaml
authorization:
  oauth-enabled: false
```

2. **Указать локальный Администратор**
```yaml
hotels-administrator:
  mode: TARGETS
  targets: localhost:29855
```

3. **Указываем свободный порт**
```yaml
server:
  port: 8086
```

Сваггер будет находиться [тут](http://localhost:8086/swagger-ui.html)