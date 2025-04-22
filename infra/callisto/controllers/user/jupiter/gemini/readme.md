Точка входа: ipvs-балансер gemini.search.yandex.net 
([определен в racktables](https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=4931)).
Соединения распределяются локально – в тот же ДЦ (man, vla, sas), где находится клиент.

Бэкенды ipvs-балансера управляются 
[awacs-балансером](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/gemini.search.yandex.net/show/).
В свою очередь, awacs-балансер отправляет запросы в случайный 
[searchproxy](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_gemini_searchproxy/)
в том же ДЦ.