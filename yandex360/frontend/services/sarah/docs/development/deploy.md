Деплой релизного пакета на окружения

- [Prestable окружение](https://deploy.yandex-team.ru/stages/sarah_prestable)
- [Production окружение](https://deploy.yandex-team.ru/stages/sarah_stable)

Сначала пакет ставится на prestable. Для этого:
1) После запуска [npm run package](./package.md#сборка-пакета) с параметрами запускается джоба в New CI, результатом работы которой будет ресурс.
Джобу можно найти в интерфейсе [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/actions/launches?dir=yandex360%2Ffrontend&id=release), указав в поле `Select branch` название ветки `releases/psfront/sarah/vX.Y.Z`.

2) После того как джоба собралась, ищем нужный ресурс и копируем его id [пример](https://jing.yandex-team.ru/files/ekhurtina/2020-08-10%2011-46-40%20Trendbox%20-%20sarah-v1.8.3%20-%20%5BSARAH%5D%20%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0%20%D0%B8%20%D0%BF%D1%83%D0%B1%D0%BB%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F%20%D1%81%D1%82%D0%B0%D1%82%D0%B8%D0%BA%D0%B8%20%D0%B8%20%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%B0%20-%20overview.png)

3) Открываем [prestable окружение](https://deploy.yandex-team.ru/stages/sarah_prestable), нажимаем `Edit`, выбираем нужный по номеру `prestable`

4) На вкладке `Disks, volumes and resources` обновляем слой (`Layer`) с `ID: front_app` [вот так](https://jing.yandex-team.ru/files/kri0-gen/2022-01-31_19-19-52.png)
   - если в релизе есть задачи с восклицательным знаком - смотрим в них, там могут быть указания, что нужно сделать кроме обновления слоя с приложением
   - если нужно обновить докер-образ, то это нужно сделать в каждом `Box`-е обновляемого `DeployUnit`-а

5) Деплоим - нажимаем жёлтую кнопку, проверяем `Diff`, пишем в комментарий релизный тикет и жмём `Deploy`

Подобным образом обновляем и деплоим на [production окружение](https://deploy.yandex-team.ru/stages/sarah_stable), с той разницей, что сначала раскатываем DeployUnit `sarah-standalone`,
смотрим на графики и если всё хорошо, то раскатываем DeployUnit `sarah`
