Здесь лежит исходный код кубиков, которые умеют реплицировать таблички с YT на GP и обратно через сервис [gptransfer](https://wiki.yandex-team.ru/dmp/tools/greenplum/gptransfer-service/manual/). При желании можно использовать скрипты в качестве консольных утилит, а не через кубик.

Кубики:
* [YT->GP](https://nirvana.yandex-team.ru/alias/operation/gptransfer-yt-gp). Файл `yt_to_gp.py` нужно прикладывать как ресурс с названием `yt_to_gp.py` при выпуске новой версии кубика.
* [GP->YT](https://nirvana.yandex-team.ru/alias/operation/logdata-gptransfer-gp-yt). Файл `gp_to_yt.py` нужно прикладывать как ресурс с названием `gp_to_yt.py` при выпуске новой версии кубика.
