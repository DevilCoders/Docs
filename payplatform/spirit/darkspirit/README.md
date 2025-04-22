# Darkspirit

<a href="https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Spirit_Darkspirit_Testing&guest=1">
  <img src="https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Billing_Spirit_Darkspirit_Testing)/statusIcon"/>
</a>

Darkspirit - сервис, позволяющий:

* (пере)регистрировать кассы в налоговой;
* поддерживать смены открытыми;
* принимать чеки от сервисов и складывать их в MDS-S3;
* отдавать чеки;
* откатывать дубликаты чеков.

Всё, необходимое для развёртывания, находится [тут](https://teamcity.yandex-team.ru/project.html?projectId=Billing_Spirit_Darkspirit&tab=projectOverview).

Основан на [yb-servant-skeleton](https://github.yandex-team.ru/Billing/yb-servant-skeleton).

Для того чтобы выложить пакет с liquibase, надо [собрать пакет](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Spirit_Darkspirit_Deploy_Liquibase), дождаться [переиндексации пакетов в RHEL](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Tools_BuildPackage_InstallIndexRpm) и добавить `yb-ds-before/yb-ds-after` в тикет кондуктора (перед этим пакеты должен быть выложены в тест, для чего стоит создать отдельный тикет).

Среда | URL
--- | ---
Тестовая | <https://greed-tm.paysys.yandex.net:8616>
Продакшн | <https://darkspirit.paysys.yandex.net:8616>

[Полезные SQL-запросы.](https://wiki.yandex-team.ru/balance/spirit/balance/spirit/DarkSpirit/sql/)

## Регистрация

1. Вызов `/v1/registrations/create-applications` создаёт записи в `t_registration` и возвращает заявления о регистрации для ФНС
2. Вызов `/v1/registrations/configure` записывает РНМы из переданного файла в `t_registration` и конфигурирует кассы, используя информацию из `t_registration`
3. Вызов `/v1/register` пробивает отчёт о регистрации в указанных кассах и меняет состояние регистрации на `REGISTRATION_COMPLETED`
4. Вызов `/v1/create-fiscalization-xml` возвращает отчёты о регистрации для указанных касс

## Замена фискальных накопителей

1. Накапливается n касс, в ФНах которых закончилось место. DS пробивает в таких кассах отчёты о закрытии ФН (`CloseFNReport`).
2. DS (`/v1/admin/create-tickets-for-replacing-fss`) зажигает лампочки и создаёт тикеты в очереди [ITDC](https://st.yandex-team.ru/ITDC), привязывая их к [царь-тикету](https://st.yandex-team.ru/SPIRIT-407).
3. Инженеры в ДЦ меняют ФНы в кассах.
4. Касса просыпается в состоянии `FATAL_ERROR` (`"fatal_reasons": ["ФН не прошёл проверку"]`). Состояние ФН — `READY_FISCAL` (так быть не должно?).
5. DS удаляет (`/v1/admin/clear-crs-with-replaced-fs`) данные, в том числе о ФН, из СУБД кассы.

## Перерегистрация

1. Вызов `/v1/reregistrations/reregister-batch` создаёт запись в `t_registration`, конфигурирует кассу и пробивает документ о перерегистрации.
