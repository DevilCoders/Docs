# Фронтенд сервиса Панель администратора Яндекс.Чаевые

Сервис для администратора и получателя чаевых

## Локальная разработка
- копируем файл `.tvm.default.json` в файл `.tvm.json`, добавляем туда секрет (получить ссылку на секрет можно у [@alexei-kliuev](https://staff.yandex-team.ru/alexei-kliuev), [@liptonicetea](https://staff.yandex-team.ru/liptonicetea), либо у кого-то из [tvm-менеджеров тут](https://abc.yandex-team.ru/services/edafronteatstipsadmin/))
- `npm install`
- `npm run dev`

В коммит-месседже указываем номер задачи, например `TIPSFRONT-000: фикс параметров`

Если нужно раскатить ветку на тестинг добавляем пул-реквесту лейбл `taxi/deploy:testing`.

## Бэкэнд для локальной разработки
Для локальной разработки по умолчанию используется тестинг бэкэнда - https://tips.eda.tst.yandex.net/

Есть локальные серверные моки на уровне сервера разработки - изменить их конфигурацию можнь в файле `tips/tools/admin/mock-server/index.js`

Есть локальные фронтовые моки, перехватывающие запросы к бэкэнду - изменить их конфигурацию можно в файле `tips/src/admin/mocking/rules.ts`

В пул-реквестах все моки должны быть выключены. Включаются по необходимости в фича-ветках.

## Релиз
Для релиза создается релизный тикет - обычный тикет с перечислением задач, которые войдут в релиз.

Задачи, которые должны войти в релиз, мержатся в `dev/eda-front-eats-tips-admin`, от него же отводится релизная ветка вида `eda-front-eats-tips-admin/TIPSFRONT-000`, с идентификатором релизного тикета `TIPSFRONT-000`.

Делается ПР из релизной ветки в мастер. Релизная ветка раскатывается на тестинг.

После тестирования ПР из релизной ветки мержится в мастер.

Запускается релиз тут - [Stable](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_FrontendMonorepo_Stable?branch=eda-front-eats-tips-admin&buildTypeTab=overview&mode=builds#all-projects)

## Тестинг
- [тестинг сервиса через старую админку и фреймы](https://tips.eda.tst.yandex.net/vhod-na-sajt.html)
- [тестинг сервиса непосредственно](https://admin.tips.eda.tst.yandex.net/) (предпочтителен до появления фреймов)
- [тестинг сервиса с фронтовыми моками](http://front-eats-tips-admin.eda.tst.yandex.net/)

## Логирование
- [проект на error.yandex-team](https://error.yandex-team.ru/projects/eda-front-eats-tips-admin/)
- [настройка](https://wiki.yandex-team.ru/error-booster/error-how-to/#browserjs)

## Ссылки
- [Сервис в админке сервисов](https://tariff-editor.taxi.yandex-team.ru/services/36/edit/356092/info)
- [Wiki сервиса](https://wiki.yandex-team.ru/eda/dev/web/tips-admin/)
