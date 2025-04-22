#### Локальный запуск
1. Собираем образ `releaser build -v docker-compose`
2. Проставляем пароль до базы и tvm секрет в `docker-compose.yml`
3. Запускаем `docker-compose up`
4. Для запуска в qyp используем `docker-compose -f docker-compose.yml -f docker-compose.qyp.yml`
