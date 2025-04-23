## Релизы

1. Отвести от свежего master-а релизную ветку (например, release/v0.0.1)

1. Выполнить команду `npm version minor`

1. Запушить изменения `git push origin --tags`

1. На пуш тэга в трендобксе запустится сборка docker-образа, после успешной сборки он автоматически выкатится в testing и rc.
    * https://deploy.yandex-team.ru/stages/testing_ohio-www
    * https://deploy.yandex-team.ru/stages/rc_ohio-www

1. Тестируем релиз (уточняем у менеджера сами или тестировщиком)

1. Катим вручную новый образ в прод – https://deploy.yandex-team.ru/stages/prod_ohio-www
**ВАЖНО! В этот момент НЕЛЬЗЯ ставить галку Update Network Bandwidth Guarantee!**

1. После выкладки в прод наблюдаем за приборами и убеждаемся, что все ок.
    * [Error-booster](https://error.yandex-team.ru/projects/passport-order-history/projectDashboard)
    * [RUM](https://rum.yandex-team.ru/projects/passport-order-history/projectDashboard)
    * [5xx](https://yasm.yandex-team.ru/alert/5xx_ohio-www_errors)
    * [4xx](https://yasm.yandex-team.ru/alert/4xx_ohio-www_errors)

1. Если что-то пошло не так, то откатываем релиз на предыдущую версию.
