# YASM сигналы

## Примеры панелей
* [Overall](https://yasm.yandex-team.ru/template/panel/MAXWELL/)
* [Информация по отдельной джобе](https://yasm.yandex-team.ru/template/panel/MAXWELL-JOB/name=reboot-segment-prestable-def/)
  > в контекст написать имя джобы, например `name=reboot-segment-prestable-def`
* [Панель с алертами переполнения WARN audit set во всех джобах](https://yasm.yandex-team.ru/template/panel/maxwell-audit-windows/)

## Шаблоны алертов
* [Шаблон алерта переполнения WARN Audit set](https://yasm.yandex-team.ru/template/alert/maxwell_audit-window-overflow/)
  > при переполнении WARN Audit set джоба останавливается до тех пор до тех пока колличество тасков станет меньше `audit_set_window`
* [Шаблон алерта переполнения Working set](https://yasm.yandex-team.ru/template/alert/maxwell_window-overflow/)

## Сигналы
* unistat-maxwell-running_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Колличество тасков в state=running
* unistat-maxwell-overflow_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Колличество тасков в state=waiting
* unistat-maxwell-window_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Размер окна джобы
* unistat-maxwell-window-overflow_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Размер overflow окна джобы
* unistat-maxwell-processed_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Колличество обработанных джобой тасков
* unistat-maxwell-remaining_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Колличество оставшихся в pool тасков

* unistat-maxwell-enforced_attt `tier=<job-name>` `deploy_unit=<pre, stable>`

  Колличество тасков завершившихся с enforce
