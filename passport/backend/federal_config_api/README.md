## Хранилище конфигов федераций
Родительский тикет: https://st.yandex-team.ru/PASSP-34864

ABC: https://abc.yandex-team.ru/services/passp-federal-config-api/

Дизайн-дока: https://wiki.yandex-team.ru/konstantinmerenkov/dd-federal-config/

TVM production: [2032890](https://abc.yandex-team.ru/services/passp-federal-config-api/resources/?view=consuming&layout=table&supplier=14&show-resource=40586040), testing: [2032888](https://abc.yandex-team.ru/services/passp-federal-config-api/resources/?view=consuming&layout=table&supplier=14&show-resource=40586039)

Секреты [для тестинга](https://yav.yandex-team.ru/secret/sec-01ft928drd2cpcesyqqezvs7ys/explore/versions)


### Цель
Централизованное место управления конфигами федераций для паспорта, 360 и возможно других

### Как запустить локально
```
docker run --name fed-postgres -p 5432:5432 -e POSTGRES_PASSWORD=foobar -d postgres
```

```
psql -U postgres -h localhost

+ копипаста из schema.sql
```

### Архитектура
Проект построен по [Hexagonal architecture](https://en.wikipedia.org/wiki/Hexagonal_architecture_(software)).

Структура кода:
```
корень проекта
  \--- cmd:
  |   Бинарник, запускающий микросервис
  |
  \--- config:
  |   Конфиги для разных окружений: development, testing, production
  |   Читаются на старте приложения. Без конфига приложение нельзя запустить.
  |
  \--- internal:
  |   |
  |   \--- core:
  |   |  |
  |   |  \--- models:
  |   |  |   Структуры сущностей, которыми оперирует сервис. В нашем случае это конфиг и его атрибуты.
  |   |  |
  |   |  \--- interfaces:
  |   |  |   Описание интерфейсов для взаимодействия controllers и adapters.
  |   |  |
  |   |  \--- controllers:
  |   |      Куски бизнес-логики, которые оперируют высокоуровневыми понятиями (models).
  |   |      Работают с adapters.
  |   |
  |   \--- federalcfgapi:
  |   |   Само веб-приложение и хендлеры, инициализация всех компонент, ...
  |   |
  |   \--- adapters:
  |       Низкоуровневая реализация CRUD конфигов, походов в ЧЯ.
  \--- mocks:
      Тут лежат моки. Они сгенерированны с помощью mockgen.
```

### Генерация моков
```
cd mocks
ya tool mockgen -package mock_adapters -source ../internal/core/interfaces/adapters.go -destination mock_adapters/mock_adapters.go
ya tool mockgen -package mock_controllers -source ../internal/core/interfaces/controllers.go -destination mock_controllers/mock_controllers.go
```
