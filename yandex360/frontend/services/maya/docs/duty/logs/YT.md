Наши логи duffman и nginx записываются на эфемерный диск, с эфемерного диска они считываются пушклиентом и отправляются в логброкер, логброкер отправляет данные в логфеллер, а он в YT.

### Полезные ссылки
* [Push client](https://wiki.yandex-team.ru/logbroker/docs/push-client/)
* [Logbroker](https://wiki.yandex-team.ru/logbroker/)
* [Logfeller](https://wiki.yandex-team.ru/logfeller/)
* [Как все это подключить](https://wiki.yandex-team.ru/logfeller/connection/)

### За что мы отвечаем
* Конфиг для push-client и его запуск на машинке. Здесь есть важный момент - чтобы отправка работала, необходима сетевая дырка до логброкера и его tvm id в настройках tvm в qloud.
* Настройку топиков в логброкере. Осуществляется через консольную утилиту [logbroker](https://wiki.yandex-team.ru/logbroker/docs/config/). Наши топики в calendar-yt/maya и calendar-public/maya, где calendar-yt и calendar-public - аккаунты, за них отвечает бэк календаря, а maya - папка.
* Настройку режима индексации и сборки, парсеры для наших логов в логфеллере. Изменения вносятся через аркадию. По работе с аркадией может подсказать бэк календаря.

### Логи в YT
* [calendar-yt-maya-duffman-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/calendar-yt-maya-duffman-access-log)
* [calendar-yt-maya-duffman-http-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/calendar-yt-maya-duffman-http-log)
* [calendar-yt-maya-nginx-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/calendar-yt-maya-nginx-access-log)
* [calendar-public-maya-duffman-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/calendar-public-maya-duffman-access-log)
* [calendar-public-maya-duffman-http-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/calendar-public-maya-duffman-http-log)
* [calendar-public-maya-nginx-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/calendar-public-maya-nginx-access-log)