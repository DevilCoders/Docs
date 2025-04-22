====Задачи в тикете:
* Выработка плана проведения работ 
  * Текущий план: https://delta.yandex-team.ru/page/epad/page/ayumrwdrkttcngi9 
* Доработка и тестирование инструментария SRE Wall-e
  * доработка типов тасок под power off/power on

====Спеки и хостлисты
* первоначальная спека хостов от sereglond@ ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28549418? drills-234_orig.txt))
* спека с разбивкой под wall-e проекты (только rtc хосты) ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28549436? drills-234_host_per_wall-e_project.txt))
* yaml-спека на выключение хостов ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28549260? drills-234_power_off.yaml))
* yaml-спека на включение хостов ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28549261? drills-234_power_on.yaml))
* дамп состояний всех хостов vla1 (name,project,inv,geo_location,state,status,health,ticket) ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28603316? fulldump.txt)) (вывод команды: %%wall-e -b hosts list -G 'RU|VLADIMIR|ALPHA|VLA-01' -t rtc -L200000 -C name,project,inv,geo_location,state,status,health,ticket%%
* !!diff!! на 87 хостов которые отсутствуют в первоначальной выборке https://paste.yandex-team.ru/3958471/text в DRILLS-234 ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28603318? diff.txt))
* допспека !!diff!! на выключение ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28603323? drills-234_power_off_additional87.yaml))
* допспека !!diff!! на включение ((https://st.yandex-team.ru/WALLESUPPORT-1314/attachments/28603322? drills-234_power_on_additional87.yaml))
* noop сценарии на пачку хостов + !!diff!! https://wall-e.yandex-team.ru/scenarios?q=drills-234&status=created%2Cfinished%2Cpaused%2Cstarted



====Инструментарий
* Rebootctl https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/rebootctl
* yandex-ipmitools  - yaipmi
* sky
* wall-e scenario !!Проблема!! (?) сценарии не расчитаны под отображение более 1000 хостов.

====Запасной план
* используем параллельный запуск ((https://raw.github.yandex-team.ru/HaaS/yandex-ipmi-client/master/yaipmi yaipmi)) ((https://wiki.yandex-team.ru/dca/services/ipmiproxy/ipmiproxy-client-cli/ дока тут))
<{базовый набор комманд для ipmitool
* yaipmi -H some.search.yandex.net power status
* yaipmi -H some.search.yandex.net power off
* yaipmi -H some.search.yandex.net power on
токен должен быть посетан в ~/.yaipmirc
}>
* sky run на которые не зашатддаунились по ipmi !!Продумать!! тк если хост не уходит с ipmi значит с ним совсем не хорошо и он потенциально уже ITDC тикет.


====Emergency
Чатик координации: https://h.yandex-team.ru/?https%3A%2F%2Ft.me%2Fjoinchat%2FBeUD0j2mYb1JKOlWs1gc7A
Для ускорения ITDC инженеров по конкретным хостам: https://staff.yandex-team.ru/ssudakov?from=suggest (Предварительная договоренность на починку YT кластеров в первую очередь получена)
