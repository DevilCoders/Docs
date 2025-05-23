# Сохранение query_args в базе данных

## Данный подраздел рассказывает о сохранении параметров URL-адресов (query_args) с учетом их значимости в базе данных Yacobot-сервера {#about}

В настоящее время в Фокусировщике реализовано два параллельных процесса записи query_args в базу данных Yacobot-сервера, так как query_args могут поступать на Yacobot-сервер как в составе URL-адресов напрямую с Master Server (1), так и из таблицы `query_args` (2). Важно, что из таблицы `query_args` в базу данных передаются только параметры, определенные, как незначимые.

![](images/pathargname.png)

(3) Для параметра в составе URL-адресов, поступившего напрямую с Master Server (для таких query_args не проводилось никаких проверок значимости) проверяется наличие в таблице `path_arg_name`.

Формат таблицы `path_arg_name`:

* `<name>` — имя параметра;
* `<path>` — hash от `path`;
* `<significant>` — значимость параметра («0» - незначимый, «1» — значимый);
* `<timestamp>` — время записи в таблицу `path_arg_name`.

Запись в таблицу производится по следующему принципу:

* если параметр уже есть в таблице `path_arg_name`, то проверяется его значимость:
    
    * если параметр определен как незначимый (`significant` = 0), то он исключается из состава URL-адреса при записи в таблицу `url`;
    * если параметр определен как значимый (`significant` = 1), то он сохраняется в составе URL-адреса при записи в таблицу `url`.
    
* если параметра нет в таблице `path_arg_name`, то он записывается в эту таблицу как значимый (`significant`=1); также этот параметр будет сохранен в составе URL-адреса при записи в таблицу `url`;

(4) Параллельно в таблицу `path_arg_name` записываются данные о query_args, определенных как незначимые на основании вычислений в модуле qargfilter. В случае если параметр уже есть в таблице `path_arg_name`, значение `significant` в таблице `path_arg_name` всегда заменяется в соответствии со значением `significant` из таблицы `query_args` (значение в `query_args` >=0.95 — значение в `path_arg_name` =«0», значение в `query_args` <0.95 — значение в `path_arg_name` =«1»).

Таким образом, в базе данных Yacobot-сервера с параметрами URL-адресов связаны две таблицы:

* таблица `path_arg_name`, в которой хранятся все параметры URL-адресов и данные об их значимости;
* таблица `url`, в которой хранятся URL-адреса для скачивания, содержащие только значимые параметры.

