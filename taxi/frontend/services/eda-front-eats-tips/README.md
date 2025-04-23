# Платежная страница Яндекс Чаевых + Чека + b2b

Сервис для пользователя, который хочет оставить чаевые в каком-то заведении (ресторан, парикмахерская, отель и тому подобное)

## Локальная разработка
- копируем файл `.tvm.default.json` в файл `.tvm.json`, добавляем туда секрет (получить ссылку на секрет можно у кого-то из [tvm-менеджеров тут](https://abc.yandex-team.ru/services/edafronteatstips/))
- `npm install`
- `npm run dev`

Для разработки отводим от `trunk` ветку вида `TIPSFRONT-000` (очередь и номер задачи из трекера).

В коммит-месседже указываем номер задачи, например `EDAWWW-1668: фикс параметров yandexpay`. Пушим ветку.

## Пул-реквест

Перед созданием пул-реквеста рекомендуется ребейзнуть ветку на trunk и сквошнуть ветку. Это можно сделать находясь в своей ветке одним из двух способов:

Первый способ:
- `arc rebase trunk`
- `arc rebase -i trunk` - и в открывшемся окне редактирования указываем операцию `s` для всех коммитов кроме первого.

Второй способ:
- `arc rebase trunk`
- `arc reset --soft $(arc merge-base trunk HEAD)` - после этого все ваши изменения в файлах выносятся на стейдж и их надо закомитить новым коммитом.

Далее создаем пул-реквест используя команду вида `arc pr create --push -m "TIPSFRONT-000: заголовок задачи"`.

Если нужно раскатить ветку на тестинг добавляем пул-реквесту лейбл `taxi/deploy:testing`.

Раскатываем ветку на тестинг [тут](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomTesting?branch=eda-front-eats-tips&mode=builds)

## Бэкэнд для локальной разработки
Для локальной разработки по умолчанию используется тестинг бэкэнда - http://eats-tips-payments.eda.tst.yandex.net/

Есть локальные серверные моки на уровне сервера разработки - изменить их конфигурацию можно в файлах:
- `tips/tools/payments/mock-server/index.js` - платежная страница
- `tips/tools/merc/mocks/index.js` - чек
- `tips/tools/corp/mocks/index.js` - b2b

Есть локальные фронтовые моки, перехватывающие запросы к бэкэнду - изменить их конфигурацию можно в файле `tips/src/payments/mocking/rules.ts` (deprecated)

В пул-реквестах все моки должны быть выключены. Включаются по необходимости в фича-ветках.

## Тестинг
- [тестинг платежной страницы Чаевых](https://eats-tips-authproxy.eda.tst.yandex.net/guest)
- [тестинг Чека](https://testing.eda.tst.yandex.ru/inplace/menu/checkout?uuid=fake-uuid)
- [тестинг b2b](https://testing.eda.tst.yandex.ru/inplace/corp/pay)

## Прод
- [платежная страница Яндекс Чаевых](https://tips.yandex.ru/guest)
- [демонстрационный ресторан в Чеке](https://eda.yandex.ru/inplace/menu?uuid=yandex-expo-table-1)
- [страница qr-оплаты b2b](https://eda.yandex.ru/inplace/corp/pay)

## Логирование
- [платежная страница на error.yandex-team.ru](https://error.yandex-team.ru/projects/eda-front-eats-tips/)
- [настройка error booster](https://wiki.yandex-team.ru/error-booster/error-how-to/#browserjs)

## Жучок
- [форма](https://forms.yandex-team.ru/ext/admin/10034310)
- [настройка](https://wiki.yandex-team.ru/bughunter/bugs/instruction/)

## Дежурство
- [Описание дежурства](https://wiki.yandex-team.ru/eda/dev/web/inplace/duty/)
- [График дежурств по сервису](https://abc.yandex-team.ru/services/edafronteatstips/duty)

## Ссылки
- [Лендинг для партнеров](https://tips.yandex/)
- [Сервис в админке сервисов](https://tariff-editor.taxi.yandex-team.ru/services/36/edit/355719/info)
- [Wiki платежной страницы Чаевых](https://wiki.yandex-team.ru/eda/dev/web/tips/)

## Танкер
- [танкер платежной страницы Чаевых](https://tanker.yandex-team.ru/project/eats/keyset/eats-tips?branch=master&statuses=*%3D)
- [танкер Чека](https://tanker.yandex-team.ru/project/eats/keyset/eats-inplace?branch=master&statuses=*%3D)
- [танкер банков Чека](https://tanker.yandex-team.ru/project/eats/keyset/eats-inplace_banks?branch=master&statuses=*%3D)
- [танкер b2b](https://tanker.yandex-team.ru/project/eats/keyset/eats-corp?branch=master&statuses=*%3D)

## Бункер
- [бункер платежной страницы Чаевых](https://bunker.yandex-team.ru/tips/payments)
- [бункер Чека](https://bunker.yandex-team.ru/eats-web/inplace)
- [бункер b2b](https://bunker.yandex-team.ru/eats-web/corp)