# flight-extras
Дополнительная информация о рейсах (passenger-experience, sky guru и т.д.)

## Разразботка

```
$ cp tools/samples/environments.sh tools/environments.sh
$ vi tools/environments.sh
$ ./tools/run-alembic.sh upgrade head
$ ./tools/run-dev.sh
```

### Изменение структуры БД

```
$ ./tools/run-alembic.sh upgrade head
vi application/models.py
$ ./tools/run-alembic.sh revision --autogenerate -m '<name>'
$ ./tools/run-alembic.sh upgrade head
```
