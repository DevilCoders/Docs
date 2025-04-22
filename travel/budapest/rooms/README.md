# Сайт продаж проекта Будапешт

[Открытые вопросы по API](TODO.API.md)

## База Данных PostgreSQL
### dev pg кластер
1. Старт локальных БД
   ```bash
   ROOMS_ROOT="${ARCADIA_ROOT}/travel/budapest/rooms"
   cd "${ROOMS_ROOT}/rooms-dev-pg-docker"
   docker-compose up --build --detach
   ```
2. Остановка локальных БД
   ```bash
   ROOMS_ROOT="${ARCADIA_ROOT}/travel/budapest/rooms"
   cd "${ROOMS_ROOT}/rooms-dev-pg-docker"
   docker-compose down -v
   ```
3. [`rooms-dev-pg-docker/postgres/rooms-hotels.sql`](rooms-dev-pg-docker/postgres/rooms-hotels.sql)

   создание и первичная настройка БД rooms-hotels, с пользователями и расширениями

4. [`rooms-dev-pg-docker/postgres/rooms-offers.sql`](rooms-dev-pg-docker/postgres/rooms-offers.sql)

   создание и первичная настройка БД rooms-offers, с пользователями и расширениями

### Накат скриптов flyway
1. Накат для базы `rooms_hotels`
   ```bash
   ROOMS_ROOT="${ARCADIA_ROOT}/travel/budapest/rooms"
   cd "${ROOMS_ROOT}/rooms-migration-db"
   ya make
   ./bin/rooms-migration-db-simple-runner.py \
        --spring.profiles.active=rooms_hotels,dev \
   # end-of-command
   ```

2. Накат для базы `rooms_offers`
   ```bash
   ROOMS_ROOT="${ARCADIA_ROOT}/travel/budapest/rooms"
   cd "${ROOMS_ROOT}/rooms-migration-db"
   ya make
   ./bin/rooms-migration-db-simple-runner.py \
        --spring.profiles.active=rooms_offers,dev \
   # end-of-command
   ```

3. TODO добавить запуск комманд flyway, info, repair итд.

## Другии комманды

1. генерация проекта IDEA
   ```bash
   ROOMS_ROOT="${ARCADIA_ROOT}/travel/budapest/rooms"
   IDEA_ROOT="${ARCADIA_ROOT}/../idea"
   cd "${ROOMS_ROOT}/"
   ya ide idea \
      --project-root=${IDEA_ROOT}/travel-budapest-rooms \
      --iml-in-project-root \
   # end-of-command
   ```
