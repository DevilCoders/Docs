# Написание миграций для создания таблиц в YT

Делается сприптом [yt_create_table.py](https://a.yandex-team.ru/arc/trunk/arcadia/adv/tools/yt/create_table/yt_create_table.py)
Основная документация на скрипт [yt-create-table.md](../../guide/jeri/yt-create-table.md)

Команды

```bash
# Качаем файл со схемой
SVN_SSH="ssh -i /etc/direct-tokens/ssh-rsa_robot-direct-arc-p" /usr/bin/svn export 'svn+ssh://robot-direct-arc-p@arcadia.yandex.ru/arc/trunk/<путь к файлу>@<ревизия>' <файл со схемой>

# Создаем таблицу
YT_TOKEN=`cat /etc/direct-tokens/yt_robot-direct-yt` yt_create_table -r --cluster $MASTER_CLUSTER --replica-clusters $SLAVE_CLUSTER1 $SLAVE_CLUSTER2 --table <//home-путь-к-таблице> --schema-file <файл со схемой>
# $MASTER_CLUSTER - кластер с реплицируемой мета-таблицей
# $SLAVE_CLUSTER[1-2] - кластера реплик (куда собственно реплицируются данные)
```

Пример миграции с пересозданием таблицы [DIRECTMIGR-1194](https://st.yandex-team.ru/DIRECTMIGR-1194)
