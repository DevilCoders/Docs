Этот файл транслируется на Вики: https://wiki.yandex-team.ru/users/maryz/DaaS-biblioteka/

==Что это==
Речь идет о питонячей библиотеке для взаимодействия с DaaS'ом. 

==Как это работает==
Происходит эмуляция запросов как в браузере. Приложение DaaS'а на эти запросы специальным образом реагирует (отдает json ответа вместо рендеринга страницы).

==Как этим пользоваться==

1. Счекаутить библиотеку:
%%
$ svn co "svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/tools/daas/daas/api"
$ cd api
$ ls
lib.py  sample.py  utils.py
%%

**lib.py** — собственно, библиотека
**sample.py** — пример сценария
**utils.py** — не очень интересные для пользователя внутренности


2. Запилить объект %%DaasApi%%. Для его инициализации необходимы и достаточны 2 параметра — инстанс дааса, на котором вы хотите что-то делать, и ваш username:
%%(python)
daas_url = 'daas.market.yandex.net'
user = 'user'
api = DaasApi(daas_url, user)
%%

Далее все действия с удаленным даасом нужно делать через объект api.

3. Делать запросы

Что сейчас можно делать:
* %%upload_file%% — загрузить файл из вашей локальной файловой системы. По сути произойдет то же самое, что и при выборе файла в браузере.
* %%fetch_report%% — загрузить репорт.
* %%enqueue_report%% — встать в очередь на кластере.
* %%remove_report%% — удалить репорт.
* %%create_task%% — создать таск на простукивание. Внимание, очень много параметров. При указании параметров как в **sample.py** репорт поднимется и опустится сам.
* %%create_diff%% — создать таск на построение диффов.
* %%view_task_output%% — посмотреть выдачу из простукивания. request_id — число от **0** до **кол-во_запросов - 1**.
* %%get_diff%% — посмотреть дифф.
* %%pause_task%% — поставить на паузу простукивание по task_id

Ожидалки:
* %%wait_queue_eternally%% — дождаться очереди для разворачивания репорта пользователем.
* %%wait_report_runnable%% — дождаться, пока репорт перейдет в состояние, в котором его можно запустить (на самом деле это возможно лишь в статусе FETCHED).
* %%wait_report_removable%% — дождаться, пока репорт перейдет в состояние, в котором его можно удалить.
* %%wait_task_done%% — дождаться завершения таска c таймаутом (deprecated).
* %%wait_task_done_eternally%% — дождаться завершения таска.
* %%wait_diff_done%% — дождаться построения диффа c таймаутом (deprecated).
* %%wait_diff_done_eternally%% — дождаться построения диффа.
Репортные ожидалки проверяют статус каждые 10 секунд в течение 3х минут, тасковая/диффная — каждую минуту в течение суток. При необходимости можно легко подхачить нужные константы в **lib.py** или же поддержать параметры в этих методах.

Это скорее всего не пригодится, но вдруг:
* %%run_report%% — запустить репорт (можно не использовать, а запускать при создании таска, см. create_task). Появился во время отладки, парный stop_report не стала делать, т.к. обнаружила, что всё есть внутри create_task.
* %%is_report_runnable%%, %%is_report_removable%%, %%is_task_done%%, %%is_diff_done%% — проверить, находится ли репорт/таск/дифф в нужном состоянии. Возвращает True/False. Используется в ожидалках.

Параметры действий смотреть в **lib.py**, а начинать можно с постепенной правки **sample.py**. И помните — всё, как в браузере (ну почти). Если какие-то параметры непонятны, всегда можно попробовать подсмотреть в интерфейс.

Если что-то пойдет не так, библиотека очень постарается человекочитаемо сругаться.
На всякий случай все действия немного логируются в файл %%api_lib.log%% (можно отследить в **lib.py**). В случае возникновения упячки для понимания, в какой момент всё упало, можно попробовать обратиться к нему.
