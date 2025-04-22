# Починка репликатора(mysql-to-yt)

## Падение при попытке обработки следующего gtid

### Возможные причины

Может возникнуть после попытки применения миграции.

### Как проявляется

Для определенного шарда приостанавливается репликация из mysql в yt.

### Как заметить 

Загорается [mysql-to-yt-full-shards-count-arnold](https://solomon.yandex-team.ru/admin/projects/direct/alerts/mysql-to-yt-full-shards-count-arnold)
Ошибка в [логвьювере](https://direct.yandex.ru/logviewer/short/gaHJajgM5AzaPu)

### Как чинить

Для починки нужно понять в каком состоянии зависла репликация. 
В yt таблице [mysql-sync-states](https://yql.yandex-team.ru/Operations/YrHEg9JwbCVQSkYTCTHQ-Oi--e5cQrJjYKGiwh3fWko=) можно найти gtid_set. 
Он состоит из списка вида: "gt_source:gt_id,...". 
gt_source можно взять из [logviewer](https://direct.yandex.ru/logviewer/short/gXTGwA8B5B9Qhg). По его gt_id можно понять, какая операция сломала репликацию. Это следующая операция за установленной в [mysql-sync-states](https://yql.yandex-team.ru/Operations/YrHEg9JwbCVQSkYTCTHQ-Oi--e5cQrJjYKGiwh3fWko=)

Исходя из операции, на которой зависла репликация и текущего состояния [mysql-sync-states.server_schema](https://yql.yandex-team.ru/Operations/YrHEg9JwbCVQSkYTCTHQ-Oi--e5cQrJjYKGiwh3fWko=) и состояния таблиц в [mysql-sync](https://yt.yandex-team.ru/arnold/navigation?path=//home/direct/mysql-sync/current/ppc:4/straight) нужно понять, какие действия смогли примениться. Для этого проверяем, что: таблицы с корректной схемой, нет лишних таблиц, server_schema корректная.

Если все действия применились, то нужно сделать gt_id++. 
Иначе, нужно откатить изменения до состояния перед попыткой применения транзакции, которая не может пройти. Обычно это изменения названий таблиц в [mysql-sync](https://yt.yandex-team.ru/arnold/navigation?path=//home/direct/mysql-sync/current/ppc:4/straight)


Если потребовалось изменить названия таблиц, необходимо приостановить действие репликатора на сломанном шарде:
```bash
yt --proxy arnold start-tx --timeout 1000000 # создает транзакцию
sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold lock --path //home/direct/m2yt/work-mode/arnold/stable/production/group-ppc:4-ppc:5-ppc:6-lock --mode exclusive --waitable --tx {id-транзакции из прошлого вызова} # лочит группу на 1000 секунд
```
Иначе есть риск, что репликатор подхватит наполовину корректные данные.

Изменить таблицы следуют в обратном порядке, относительно операциию.

Пример изменения для таблицы clients_options на четвертом шарде:
```bash
sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold unmount-table //home/direct/mysql-sync/v18.1/ppc:4/straight/clients_options

sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold move //home/direct/mysql-sync/v18.1/ppc:4/straight/clients_options //home/direct/mysql-sync/v18.1/ppc:4/straight/_clients_options_new
sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold mount-table //home/direct/mysql-sync/v18.1/ppc:4/straight/_clients_options_new

sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold unmount-table //home/direct/mysql-sync/v18.1/ppc:4/straight/_clients_options_old
sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold move //home/direct/mysql-sync/v18.1/ppc:4/straight/_clients_options_old //home/direct/mysql-sync/v18.1/ppc:4/straight/clients_options
sudo YT_TOKEN_PATH=/etc/direct-tokens/yt_robot-direct-yt yt --proxy arnold mount-table //home/direct/mysql-sync/v18.1/ppc:4/straight/clients_options
```

### Пример

https://st.yandex-team.ru/DIRECT-113845

### Эксперты

[Игорь Костромин](https://staff.yandex-team.ru/elwood), [Юрий Кабаргин](https://staff.yandex-team.ru/yukaba)
