====В сервисе обнаружены:

	<a href="#BrokenPods">1. Сломанные поды</a>

	<a href="#EvictionRequested">2. Поды с запрошенной эвакуацией</a>

Детали приведены ниже
===<p id="BrokenPods">Сломанные поды<p>
	
		В сервисе ((https://nanny.yandex-team.ru/ui/#/services/catalog/test test)) обнаружены сломанные поды. Такое случается, если:
* падает сам запускаемый в контейнере сервис
* приложение в контейнере запущено, но сломалась его внутренняя логика и теперь не проходит ((https://docs.yandex-team.ru/nanny/how-to/structured-instancectl-config#readiness проверка его статуса)).
* на хосте возникли проблемы с железом или хостовой инфраструктурой, и контейнеру стало плохо.

==== История состояний сервиса
<#
<table>
<tr>
<td></td>

<td style="text-align: center;">20 Jan 15:55 MSK</td>

<td style="text-align: center;">20 Jan 15:55 MSK</td>

<td style="text-align: center;">20 Jan 15:55 MSK</td>

<td style="text-align: center;">20 Jan 15:55 MSK</td>

<td style="text-align: center;">20 Jan 15:55 MSK</td>

</tr>
<tr>
<td>Статус снапшота</td>

<td><div title="PREPARED" style="width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="ACTIVE" style="width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="PREPARING" style="width: 160px; display: inline-block; text-align: center; background: #5bc0de; color: white; ">PREPARING</div></td>

<td><div title="DEACTIVATE_PENDING" style="width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">DEACTIVATE_PENDING</div></td>

<td><div title="GENERATING" style="width: 160px; display: inline-block; text-align: center; background: #5bc0de; color: white; ">GENERATING</div></td>

</tr>

<tr>
<td><p style="font-size: large;">Проблемные поды</p></td>
</tr>


<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-1" target="_blank">test-bromigo-1.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-1.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-2" target="_blank">test-bromigo-2.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-2.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-3" target="_blank">test-bromigo-3.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-3.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-4" target="_blank">test-bromigo-4.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-4.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-5" target="_blank">test-bromigo-5.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-5.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-6" target="_blank">test-bromigo-6.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-6.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-7" target="_blank">test-bromigo-7.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-7.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-8" target="_blank">test-bromigo-8.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-8.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-9" target="_blank">test-bromigo-9.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-9.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-10" target="_blank">test-bromigo-10.sas.yp-c.yandex.net</a><br>
Графики: <a href="https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-10.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id" target="_blank">под</a>,
<a href="https://yasm.yandex-team.ru/template/panel/Host/hosts=some-node-id" target="_blank">хост</a></td>

<td><div title="ACTIVE" style=" width: 160px; display: inline-block; text-align: center; background: #337ab7; color: white; ">ACTIVE</div></td>

<td><div title="HOOK_SEMI_FAILED" style=" width: 160px; display: inline-block; text-align: center; background: #777777; color: white; ">HOOK_SEMI_FAILED</div></td>

<td><div title="PREPARED" style=" width: 160px; display: inline-block; text-align: center; background: #5cb85c; color: white; ">PREPARED</div></td>

<td><div title="REMOVED" style=" width: 160px; display: inline-block; text-align: center; background: #f0ad4e; color: white; ">REMOVED</div></td>

<td><div title="ERROR" style=" width: 160px; display: inline-block; text-align: center; background: #dc3545; color: white; ">ERROR</div></td>

</tr>

</table>

	#>

	<{ и еще несколько подов (5)
	test-bromigo-11, test-bromigo-12, test-bromigo-13, test-bromigo-14, test-bromigo-15
	}>
	<#

#>

((https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#iss-states-definitions Легенда статусов))

==== Почему это важно?
Это может значить, что сервис сломан целиком. Но даже если это не так, мы всё равно рекомендуем починить сломанные поды.
<{Если долго не делать этого, то на других подах сервиса могут начаться регламентные работы с даунтаймом.
Все регламентные работы в облаке запускаются с учётом бюджета на ((https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/replication-policy/ переселение подов)), указываемого в %%Replication policy%% сервиса. В данный бюджет входят также все сломанные поды. Иными словами, если бюджет сервиса на переселение равен 10 подов, и в сервисе уже сломано 10 подов по каким-то случайным причинам, то ни один другой под сервиса не будет отдан в даунтайм для проведения регламентных работ. Однако есть и исключение, связанное с тем, что **таймаут ожидания запуска работ ограничен**. Поэтому если текущие сломанные поды в течение длительного времени не оживут, работы на других подах сервиса всё равно будут запущены. Это приведёт к даунтайму других подов сервиса, и суммарно в нерабочем состоянии окажется уже большее число контейнеров сервиса, и оно уже может быть критичным.}>

==== Как починить поломку?
Нужно разобраться в её причинах, для чего провести диагностику:
1. Открыть ((https://nanny.yandex-team.ru/ui/#/services/catalog/test сервис)) и почитать его ((https://nanny.yandex-team.ru/ui/#/services/catalog/test/runtime_attrs_history историю выкладок)), возможно в нём катилось что-то ломающее.
2. Посмотреть текущее состояние сломанных подов, например, ((https://nanny.yandex-team.ru/ui/#/services/pods/test/clusters/SAS/pods/test-bromigo-1 test-bromigo-1.sas.yp-c.yandex.net)) и сверить его с ((https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#iss-states-definitions легендой статусов)).
3. Зайти в контейнер пода через команду %%ssh test-bromigo-1.sas.yp-c.yandex.net%% и почитать логи инфраструктурных супервизоров: %%loop.log%%, %%loop.log.full%%, %%anamnesis.log%%. Если какой-то из процессов сервиса падает, то зачастую в этих логах можно узнать, какой именно.
4. Почитать stderr и stdout процессов сервиса, для этого как и выше зайти в контейнер пода и посмотреть файлы с расширениями %%.err%% и %%.out%%
5. Помимо логов инфраструктурных процессов есть смысл почитать логи самого запущенного сервиса, как правило они находятся в директории %%/logs%%, но могут и в другом месте, это зависит от того, как свой сервис настраивал его владелец.
6. Посмотреть графики потребления ресурсов сломанными подами, ((https://yasm.yandex-team.ru/template/panel/New-Porto-Container/hosts=test-bromigo-1.sas.yp-c.yandex.net;itype=default;nanny=test;node=some-node-id пример)). Возможно сервису перестало хватать вычислительных ресурсов, например, памяти или процессора.
7. Если по логам и графикам ничего непонятно, починить надо, но не получается, то призвать дежурного, нажав на кнопку "Призвать дежурного". Спустя какое-то время дежурный от команды Nanny поможет с диагностикой проблем.

Если сервис //штатно сломан//, например, это тестовый или временно поднятый контур, то чтобы подобные тикеты не заводились, достаточно ((https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#mark-as-testing пометить его как testing)). Но делать так с продовыми сервисами не рекомендуется, т.к. это значительно ослабит ограничения на даунтайм их подов для работ на железе.

==== Я починил под, когда закроется тикет?
Статусы подов пересчитываются раз в несколько часов (на момент последнего обновления тикета, число часов - 4). Как только сломанных подов не останется мы обязательно пришлем уведомление и закроем тикет.
	
===<p id="EvictionRequested">Поды с запрошенной эвакуацией<p>
	В вашем сервисе ((https://nanny.yandex-team.ru/ui/#/services/catalog/test/replication_policies включена политика уведомлений)) о подах, на которых запрошено переселение. Обычно эти нотификации включают, если переселение подов требует ручных действий, или чтобы просто быть в курсе о них. Если вам не нужны эти уведомления и ручное подтверждение переселения, вы всегда можете отключить их по ((https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/replication-policy/#notification-policy инструкции)).
<#
<table>
<tr>
	<td><strong>Имя пода</strong></td>
	<td><strong>Время запроса эвакуации</strong></td>
	<td><strong>Время принудительного подтверждения</strong></td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-1" target="_blank">test-bromigo-1.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-2" target="_blank">test-bromigo-2.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-3" target="_blank">test-bromigo-3.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-4" target="_blank">test-bromigo-4.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-5" target="_blank">test-bromigo-5.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-6" target="_blank">test-bromigo-6.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-7" target="_blank">test-bromigo-7.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-8" target="_blank">test-bromigo-8.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-9" target="_blank">test-bromigo-9.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp/sas/pods/test-bromigo-10" target="_blank">test-bromigo-10.sas.yp-c.yandex.net</a></td>
<td style="text-align: center;">20 Jan 15:55 MSK</td>
<td style="text-align: center;">24 Jan 15:55 MSK</td>
</tr>

</table>
#>

<{ И еще несколько подов (5)
	test-bromigo-11, test-bromigo-12, test-bromigo-13, test-bromigo-14, test-bromigo-15
}>


	


==== Мне не нравятся эти тикеты
Мы начали внедрять инфраструктуру подобных уведомлений не так давно, она может быть несовершенна и мы с радостью её улучшим. Если кажется, что наши критерии сломанности подов слишком жесткие, нотификации бесят, инструкция непонятная или что-то ещё плохо - оставьте, пожалуйста, конструктивный наброс комментом к этому тикету и призовите дежурного, нажав на кнопку "Призвать дежурного"