Описание
====
Утилита для сбора и анализа статистики по переносам квот
Данные берутся из тикетов в очереди DISPENSERTREQ

Данные из тикетов записываются в result.json
Статистика записывается в statistic.txt

--------
Запуск
====

Локально
----
Для запуска утилиты необходимо положить токен в ~/.abc/token и из папки
arcadia/infra/capacity_planning/utils/quota_transfer_statistic/  вызвать
(логин будет будет совпадать с логином компьютера):
```
ya make
./analytics
```
Либо можно передать токен и логин при запуске в качестве параметров:
```
--token <token> --login <login>
```
Также доступны параметры
```
./analytics --start-date <dd.mm.yyyy>
--end-date <dd.mm.yyyy>
--last-months <число месяцев>
```
Токен можно получить по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b)

