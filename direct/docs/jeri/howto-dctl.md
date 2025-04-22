# Утилита dctl

## Для чего нужен dctl { #purpose }

- поменять количество подов в сервисе
- добавить/убрать секреты
- ...

Делать это через веб-интерфейс Деплоя не получится: веб-интерфейс может затирать некоторые существенные поля в спеке (это баг, но он есть).

## Откуда брать бинарник { #where-it-comes-from }

Можно пользоватья `ya tool dctl`, можно собрать `dctl` из исходников ([инструкция](https://wiki.yandex-team.ru/deploy/docs/tools/dctl/#build)).

Для ppcdev и ppcback собираем пакет yandex-du-dctl ([pkg.json](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/dctl/pkg.json)), в нем бинарник `dctl`.

## Как запускать { #how-to-run }

Можно запускать локально, можно с ppcdev. 

Программа cама сгенерирует токен и положит его куда надо, подробнее см. в документации по dctl. 

## Посмотреть список "моих" стейджей { #list-my-stages }

```sh
ya tool dctl list stage
```
Пример вывода:
```
+---------+---------------------------+---------+----+------+-------+
| Cluster |             ID            | SpecRev | RS | MCRS |  Pods |
+---------+---------------------------+---------+----+------+-------+
|   xdc   |   direct-chassis-devtest  |    18   | 0  |  1   | 1/0/1 |
|   xdc   | direct-chassis-production |    14   | 0  |  1   | 0/1/1 |
|   xdc   |  direct-logviewer-devtest |    25   | 0  |  1   | 1/0/1 |
|   xdc   |     kuhtich-test-stage    |    8    | 1  |  0   | 2/0/2 |
|   xdc   |          testtest         |    36   | 1  |  0   | 4/0/4 |
|   xdc   |      zhur-test-stage      |    7    | 0  |  1   | 1/0/1 |
+---------+---------------------------+---------+----+------+-------+
```

Не очень полезное действие, т.к. не факт, что нужный стейдж будет в "моих". 
С ключом ```-a``` команда должна показывать все стейджи, но там паджинация, пользоваться неудобно. 

Проще найти нужный стейдж в [интерфейсе](https://deploy.yandex-team.ru) и взять id оттуда. Id — это часть в url после https://deploy.yandex-team.ru/stage


## Получить текущие настройки (спеку) стейджа { #get-stage-spec }

```sh
ya tool dctl get stage direct-chassis-devtest > direct-chassis-devtest.yaml
```

## Отредактировать спеку { #edit-spec }

```sh
vim direct-chassis-devtest.yaml
```

Как соотносятся ключи в yaml и поля в интерфейсе — догадываемся телепатически. 


## Применить новые настройки (спеку) стейджа { #apply-stage-spec }

```sh
ya tool dctl put stage direct-chassis-devtest.patched.yaml
```

Ревизия в спеке может оставаться старая, deploy запишет новые настройки с новой ревизией.


## Посмотреть состояние стейджа { #get-stage-status }

```sh
ya tool dctl status stage direct-chassis-devtest
```

## Разное { #unsorted }

### Копирование стейджа { #copy-stage }

Для копирования стеджа есть специальная команда copy, она делает правильное с секретами. 

Подробнее: <https://wiki.yandex-team.ru/deploy/docs/tools/dctl/#copy-stage>

Коротко:

```sh
dctl get stage old_stage > my_stage.yaml
vim my_stage.yaml # если хотим поменять какие-то параметры; id менять не надо
dctl copy stage my_stage.yaml new_stage_i
```

### Храним релизные правила в репозитории

По сохраненным спекам легко пересоздать правило или сделать аналогичное существующим. 

Файлы и короткую инструкцию см. в <https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/yadeploy>


## Ссылки { #links }

- [Документация по dctl](https://deploy.yandex-team.ru/docs/reference/tools/dctl)
- [Копирование стейджей через dctl](https://wiki.yandex-team.ru/deploy/docs/tools/dctl/#copy-stage)
- [Директовые релизные правила в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/schemata/yadeploy)
- [pkg.json для нашего пакета yandex-du-dctl](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/dctl/pkg.json)
