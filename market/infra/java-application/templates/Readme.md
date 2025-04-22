### Доступные шаблоны java приложения, которые используют СПОК

---

#### generic-template
##### Пустой java шаблон (базовое приложение)

---

#### generic-with-postgres-template
##### Добавляются конфиги подключения к ПостГресу

---

#### quartz-tms-template
##### Добавляется Quartz TMS + конфиги подключения к ПостГресу

---

#### bazinga-tms-with-mongo-template
##### Добавляется Bazinga TMS + конфиги подключения к Монге

---
##### `app_generation.sh` - можно использовать для генерации приложения по шаблону
##### `MarketJavaApplicationProducer` - продьюсер в сендбоксе
Путь в аркадии: arcadia/sandbox/projects/market/infra/MarketJavaApplicationProducer
В свою очередь продьюсер использует app_producer.py
Путь в аркадии:arcadia/sandbox/projects/market/infra/helpers/app_producer.py

Для быстрого понимания что запродьюсится используйте - `app_generation.sh`
Укажите желаемый шаблон и кастомизируйте параметры по желанию.
