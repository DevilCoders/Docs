# imPulse

Документация: https://wiki.yandex-team.ru/security/impulse/
Frontend: https://github.yandex-team.ru/security/impulse-ui

## Локальная разработка

1. Запуск контейнера с БД: ``docker run --name impulsedb -v /Users/aleksei-m/tmp/impulsedb:/var/lib/postresql/data -e POSTGRES_PASSWORD=impulse -e POSTGRES_USER=impulse -e POSTGRES_DB=impulse -p 127.0.0.1:5432:5432 -d postgres``
2. Запуск codeql-api: ``IMPULSE_ENV=dev DB_DSN="host=127.0.0.1 port=5432 dbname=impulse user=impulse" DB_PASSWORD=impulse HTTP_PORT=3003 ./codeql-api``
3. Запуск scan-api: ``IMPULSE_ENV=dev DB_DSN="host=127.0.0.1 port=5432 dbname=impulse user=impulse" DB_PASSWORD=impulse HTTP_PORT=3001 ./scan-api``
4. Запуск storage-api: ``IMPULSE_ENV=dev DB_DSN="host=127.0.0.1 port=5432 dbname=impulse user=impulse" DB_PASSWORD=impulse HTTP_PORT=3002 ./storage-api``
5. Запуск webhook: ``IMPULSE_ENV=dev DB_DSN="host=127.0.0.1 port=5432 dbname=impulse user=impulse" DB_PASSWORD=impulse HTTP_PORT=3004 ./webhook``
6. Запустить worker: ``IMPULSE_ENV=dev DB_DSN="host=127.0.0.1 port=5432 dbname=impulse user=impulse" DB_PASSWORD=impulse ./worker``
7. Запустить frontend: ``make devrun``

