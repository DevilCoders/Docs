Поды с запрошенной эвакуацией

-----


=====Поды не удалось выключить для эвакуации
В ((https://nanny.yandex-team.ru/ui/#/services/catalog/test/ сервисе)) включен ((https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/replication-policy/#shutdown-pod-policy призыв пользователя)) при невозможности выключить под для переселения. Для следующих подов было запрошено выключение, но из-за проблем с их серверами не удалось убедиться, что оно успешно завершено:
<#
<table>
<tr>
	<td><strong>Имя пода</strong></td>
	<td><strong>Время запроса эвакуации</strong></td>
	<td><strong>Время принудительного выключения</strong></td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp//pods/" target="_blank">pod-5</a></td>
<td style="text-align: center;">01 Mar 07:54 MSK</td>
<td style="text-align: center;">05 Mar 07:54 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp//pods/" target="_blank">pod-6</a></td>
<td style="text-align: center;">01 Mar 07:54 MSK</td>
<td style="text-align: center;">05 Mar 07:54 MSK</td>
</tr>

</table>
#>

<{ И еще несколько подов (2)
	pod-7, pod-8
}>


=====Не сработало штатное переселение подов
В вашем ((https://nanny.yandex-team.ru/ui/#/services/catalog/test/ сервисе)) есть поды, которые не удалось переселить штатным способом в течение 24 часов. По истечении приведённого ниже таймаута они будут выключены форсированно для проведения регламентных работ. Возможные причины следующие:
- Слишком много сломанных подов и не хватает бюджета на переселение
- Включено ручное подтверждение всех переселений
- Есть незавершённая выкладка (переселение работает только при отсутствии выкладки)
- В сервисе есть невыкаченный снэпшот и используется блокирующаяся об него ((https://docs.yandex-team.ru/nanny/reference/yp/replication-policy legacy-политика переселения))
<#
<table>
<tr>
	<td><strong>Имя пода</strong></td>
	<td><strong>Время запроса эвакуации</strong></td>
	<td><strong>Время принудительного выключения</strong></td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp//pods/" target="_blank">pod-1</a></td>
<td style="text-align: center;">27 Feb 10:54 MSK</td>
<td style="text-align: center;">03 Mar 10:54 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp//pods/" target="_blank">pod-2</a></td>
<td style="text-align: center;">27 Feb 10:54 MSK</td>
<td style="text-align: center;">03 Mar 10:54 MSK</td>
</tr>

</table>
#>

<{ И еще несколько подов (2)
	pod-3, pod-4
}>


=====Запрошено, но ещё не просрочено переселение подов
В вашем сервисе ((https://nanny.yandex-team.ru/ui/#/services/catalog/test/replication_policies включена политика уведомлений)) о подах, на которых запрошено переселение. Обычно эти нотификации включают, если переселение подов требует ручных действий, или чтобы просто быть в курсе о них. Если вам не нужны эти уведомления и ручное подтверждение переселения, вы всегда можете отключить их по ((https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/replication-policy/#notification-policy инструкции)).
<#
<table>
<tr>
	<td><strong>Имя пода</strong></td>
	<td><strong>Время запроса эвакуации</strong></td>
	<td><strong>Время принудительного выключения</strong></td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp//pods/" target="_blank">pod-10</a></td>
<td style="text-align: center;">01 Mar 10:53 MSK</td>
<td style="text-align: center;">05 Mar 10:53 MSK</td>
</tr>

<tr>
<td><a href="https://deploy.yandex-team.ru/yp//pods/" target="_blank">pod-11</a></td>
<td style="text-align: center;">01 Mar 10:53 MSK</td>
<td style="text-align: center;">05 Mar 10:53 MSK</td>
</tr>

</table>
#>

<{ И еще несколько подов (2)
	pod-12, pod-9
}>



-----

В сервисе обнаружены поды с запрошенной эвакуацией:
 - ожидающие подтверждения эвакуации при включенной политике HANDSUP (4)
 - c эвакуацией, запрошенной более 24 часов назад (4)
 - по причине ((https://nanny.yandex-team.ru/ui/#/services/catalog/test/replication_policies включенных уведомлений)) (4)
