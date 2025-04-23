# Troubleshooting
Попробуем собрать алгоритм диагностики проблем с hostmanager'ом.

# Алгоритм
Как и в любой другой поломке необходимо:
  * локализовать сбойный компонент
  * устранить причину
  
## Локализация
Эту часть можно разделить на две части:
  * локализация сбойного хоста
  * локализация сбойного компонента

# Salt states errors
К сожалению, основная причина ошибок - это проблемы с конкретными стейтами солта, которые не представляется возможным
вывести на панели (до появления достаточно развитого дэшборда).
TL;DR:
  * Пробуем разложить в yasm график по **топу хостов**:
    * [ctype=prestable](https://yasm.yandex-team.ru/template/panel/YA-SALT/ctype=prestable/1/)
    * [geo=sas](https://yasm.yandex-team.ru/template/panel/YA-SALT/geo=sas/1/)
    * [geo=vla](https://yasm.yandex-team.ru/template/panel/YA-SALT/geo=vla/1/)
    * [geo=man](https://yasm.yandex-team.ru/template/panel/YA-SALT/geo=man/1/)
    * [geo=msk](https://yasm.yandex-team.ru/template/panel/YA-SALT/geo=msk/1/)
  * Пробуем получить список хостов по **версии juggler'а** [из имеющихся агрегатов](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dhostman-salt).

Далее локализуем проблемные стейты на хосте. 

Выполняем: `ya-salt status -o short` и смотрим первые красные строчки, например:

```
$ ya-salt status -o short
 --- Salt
  ID: iss_ci_packages
   Started: 1970-01-19 07:38:43
   Duration: 972.494s
   Comment: Problem encountered installing package(s). Additional info follows:

errors:
    - E: Version '11.5ubuntu2.1' for 'build-essential' was not found
  ID: python_packages
   Started: 1970-01-19 07:38:43
   Duration: 968.837s
   Comment: Problem encountered installing package(s). Additional info follows:

```