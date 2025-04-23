Библиотека, для того чтобы выбирать мастера на основе лока в БД. На данный момент сделано только для PostgreSQL.

**Важно.** Кластеры PostgreSQL в yc по умолчанию поднимаются за pgbouncer. Из-за этого `pg_try_advisory_lock` не работает
как ожидается. Чтобы он работал, надо перевести pooling mode в `SESSION`:
```sh
SSL_CERT_FILE=~/.certs/allCAs.pem yc managed-postgresql cluster update <claster_id> --connection-pooling-mode SESSION
```
