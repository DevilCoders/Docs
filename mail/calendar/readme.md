# Графики
Каждая панель шаблонизирована параметром *env* который принимает тип окружения для которого мы хотим увидеть графики и параметром *application* который показывает для какого компонента календаря мы хотим увидеть графики\
### Calendar-YT
#### Web
[calendar-yt-web](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env=production;application=web/)\
[calendar-yt-web-routes_/](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2F/)\
[calendar-yt-web-routes_ui](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env=production;application=web_routes;routes_path=ui/)\
[calendar-yt-web-routes_/api/](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Fapi%2F/)\
[calendar-yt-web-routes_/display](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Fdisplay%2F/)\
[calendar-yt-web-routes_/internal/](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Finternal%2F/)\
[calendar-yt-web-routes_/mailhook/](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Fmailhook%2F/)\
[calendar-yt-web-routes_/soap/](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Fsoap%2F/)
#### Worker
[calendar-yt-worker](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env=production;application=worker/)
#### Caldav
[calendar-yt-caldav](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env=production;application=caldav/)\
[calendar-yt-caldav-routes](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env=production;application=caldav_routes/)
#### Alerts
[calendar-yt-alerts](https://yasm.yandex-team.ru/template/panel/Calendar-YT/env=production;application=alerts/)

### Calendar-Public
#### Web
[calendar-public-web](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env=production;application=web/)\
[calendar-public-web-routes_/](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2F/)\
[calendar-public-web-routes_ui](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env=production;application=web_routes;routes_path=ui/)\
[calendar-public-web-routes_/api/](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Fapi%2F/)\
[calendar-public-web-routes_/internal/](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env%3Dproduction%3Bapplication%3Dweb_routes%3Broutes_path%3D%2Finternal%2F/)
#### Worker
[calendar-public-worker](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env=production;application=worker/)
#### Caldav
[calendar-public-caldav](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env=production;application=caldav/)\
[calendar-public-caldav-routes](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env=production;application=caldav_routes/)
#### Alerts
[calendar-public-alerts](https://yasm.yandex-team.ru/template/panel/Calendar-Public/env=production;application=alerts/)

## Генерация алертов
[Backend](https://a.yandex-team.ru/arc/trunk/arcadia/mail/yasm)\
[DB](https://github.yandex-team.ru/mail-admin/ansible-juggler-configs)\
[Установка ansible](https://a.yandex-team.ru/arc/trunk/arcadia/mail/monitoring/delivery/ansible-juggler-configs)

# Админка
[corp-testing](https://calendar-yt-testing.common.yandex.net/admin)\
[corp-production](https://admin.calendar-yt.yandex-team.ru)

[public-testing](https://calendar-public-testing.common.yandex.net/admin)\
[public-production](https://admin.calendar-public.yandex-team.ru)

# Сборка в IDE
 - Генерируем проект: ya ide idea --directory-based --group-modules=tree --iml-in-project-root --with-content-root-modules --generate-junit-run-configurations -r `OUT_DIR`
 - Поставить плагины в IDEA: Lombok и [Arc](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij#как-установить-плагин)
 - Собираем
 - Для запуска тестов в IDEA:
 - - копируем параметры из ut/ya.make секции `JVM_ARGS` в параметры тестовой конфигурации `VM Options`
 - - берем продовый токен для staff (например, в секретах инстанса календаря /etc/yandex/calendar/secret.properties) и прописываем их в `VM Options`: `-Dyt.staff.token=%token%`
 - - берем тестовый TVM токен календаря (calendar-public.production.worker) и прописываем в `VM Options`: `-Dcalendar.tvmtool.token=%token%`
 - - для запуска caldav-compliance тестов также [нужен пароль](https://a.yandex-team.ru/arc/trunk/arcadia/mail/calendar/caldav-ut#%D1%83%D1%87%D0%B5%D1%82%D0%BD%D0%B0%D1%8F-%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D1%8C) для caldavtestuser
