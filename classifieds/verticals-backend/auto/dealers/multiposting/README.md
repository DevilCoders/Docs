# Multiposting

## Модули
- api –– API сервиса
- scheduler –– модуль, отвечающий за сбор, обогащение и хранение данных

## Тимсити
[api](https://nda.ya.ru/t/vwo20f_03thpzk)

[scheduler](https://nda.ya.ru/t/rRzHZZO03thqFt)

## Логи
[api](https://nda.ya.ru/t/wBLyD_KI3thqfC)

[scheduler](https://nda.ya.ru/t/ZPIxujfA3thqfW)

## Метрики
[Grafana](https://nda.ya.ru/t/U2GuxUo73thrrz)

[Tasks](https://nda.ya.ru/t/ESffp-MP3thrqX)

##Sentry

## Jaeger

## PostgreSQL clusters
[postgresql-test](https://nda.ya.ru/t/Ue5rrAsf3tho4M)

[postgresql-prod](https://nda.ya.ru/t/ALzEA9Ou3tho8o)

## Secrets
[s3-test](https://nda.ya.ru/t/ulZLFKrl3tho9E)

[s3-prod](https://nda.ya.ru/t/y01iYUtT3thoGD)

[postgresql-test](https://nda.ya.ru/t/NN3pwKMM3thoNs)

[postgresql-prod](https://nda.ya.ru/t/ilPQvhb43thoP4)

[zookeeper-test](https://nda.ya.ru/t/yaogpY5L3thoyx)

[zookeeper-prod](https://nda.ya.ru/t/dqYXRP8C3thpGC)

## Local run

### Scheduler
Create `application.local.conf` in `multiposting/scheduler.resources`:
```hocon
db {
  url = "jdbc:postgresql://localhost:5432/postgres"
  user = "postgres"
  password = "postgres"
}

public-s3 {
  auth {
    key = "{key}"
    secret = "{secret}"
  }
}

zookeeper {
  auth {
    password = "{password}"
  }
}

```

