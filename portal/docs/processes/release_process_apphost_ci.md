# Релиз Графов Морды в новом CI

| NB: Графы релизит только [дежурный Авокадо](https://abc.yandex-team.ru/services/home/duty/?role=3725) |
| ----------------------------------------------------------------------------------------------------- |

## Выкладка про прод
Откройте [дашборд Графов Морды](https://a.yandex-team.ru/projects/home/ci/releases/timeline?dir=portal%2Fmorda-go%2Fcmd%2Fmorda-graphs&id=morda-graphs) в Аркадийном CI.

Процесс релизов графов аналогичен релизу [Morda Go](https://docs.yandex-team.ru/portal/processes/platform_release_process)

Перед включением одного пода во VLA вооружитесь следующими панельками:
* [Общая панель дежурного Морды](https://yasm.yandex-team.ru/template/panel/morda_lights_dezh/mode=full)
* [Панелька графа ПП](https://yasm.yandex-team.ru/menu/Portal/Avocado/morda-app/apphost_template_morda_searchapp/)
* [Панелька графа десктопа/тача](https://yasm.yandex-team.ru/menu/Portal/Avocado/morda-go/apphost_template_morda_v2/)
* [Панелька подграфа Новостей](https://yasm.yandex-team.ru/menu/Portal/Avocado/morda-app/apphost_template_top_news/)
* [Панель ошибок Error Booster для Аппхоста](https://nda.ya.ru/t/18cqrds84ThBRn)
* [Панель ошибок Error Booster для Morda Go](https://nda.ya.ru/t/OZrv1V6S4fny8i)
* [Панель ошибок Error Booster c клиентскими ошибками Морды в ПП Андроид](https://nda.ya.ru/t/wLlnJuLx4ThDVg)
* [Панель ошибок Error Booster c клиентскими ошибками Морды в ПП iOS](https://nda.ya.ru/t/oP9K912L4ThEYS)

Панели необходимо просматривать при релизе в каждый из ДЦ.

## Если что-то пошло не так {when-something-goes-wrong}
1. Остановите текущую выкладку на графе CI (задания Activate)
2. Если релиз как-то влияет на пользователей, то попросите Марти в Мордячем Мартичате снять трафик Морды с локации, на которой начались проблемы (как правило, это VLA).
3. Остановите релиз в панели СI, выбрав пункт Cancel.
   ![](https://jing.yandex-team.ru/files/yanykin/platform_release_process__cancel.png =x100){: .center}
4. Если релиз успел дойти до стадии prestable

   ![](https://jing.yandex-team.ru/files/cheetah/Screenshot%202022-03-23%20at%2016.11.21.png =x250){: .center} 

   откатите релиз через панель CI, нажав Rollback to последнего успешнего релиза (как правило, предыдушего)
   ![](https://jing.yandex-team.ru/files/yanykin/platform_release_process__rollback_to.png =x100){: .center}

