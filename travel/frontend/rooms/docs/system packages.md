## Здесь инфа о пакетах, которые устанавливаются в контейнер с приложением из [этого списка](../deploy/bin/requirements)

-   cron - cron, нужен для запуска ротации логов
-   yandex-logrotate - специально обученный ротатор логов https://wiki.yandex-team.ru/logrotate/
-   yandex-lockf - пакет для создания лока, нужен для ротации логов
-   statbox-push-client-daemon - пуш клиент, нужен для отправки логов авиа https://wiki.yandex-team.ru/logbroker/docs/push-client/
-   yandex-solomon-agent-bin - соломон агент https://wiki.yandex-team.ru/solomon/agent/
-   gettext - команда envsubst https://www.gnu.org/software/gettext/manual/html_node/envsubst-Invocation.html
-   lsof - инструмент для просмотра используемых[/открытых файлов в системе
