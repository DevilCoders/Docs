# HTTP-Сервис синхронизации яндексовых кук

## где живет

### под капотом
`prod` - `af-autoru-yandex-web.vrts-slb.prod.vertis.yandex.net`

`test` - `af-autoru-yandex-web.vrts-slb.test.vertis.yandex.net`

### из браузера
В деве `https://autoruyandex.<rep name>.<user name>.dev.vertis.yandex.ru`

В тесте `https://autoru.test.vertis.yandex.ru`

В проде `https://autoru.yandex.ru`

## как работает
Если вам не надо менять код пакета, то делать ничего не надо.
Если пакет не запущен, запросы уйдут в тест.

Для дева надо настроить сетрификат для хостов в зоне .ru

В пользовательском приложении висит [мидлваря](../auto-core/models/cookieSync/middleware/redirect-to-autoru-yandex.js), которая при нужде синхронизировать с yandex.ru куку yandexuid редиректит в приложение [www-autoru-yandex](../auto-core/models/cookieSync/middleware/get-cookies-from-yandex.js) в зоне yandex.ru.
www-autoru-yandex ставит куки (если их нет), шифрует и перенаправляет в [www-desktop](../auto-core/models/cookieSync/middleware/set-yandex-cookies.js), где куки расшифровываются и устанавливаются в домен auto.ru с последующим редиректом на исходную пользовательскую страницу.

## как выкатывать
Традиционно через [TeamCity](https://t.vertis.yandex-team.ru/buildConfiguration/vs_frontend_Applications_AuroRuFrontendRepo_ReleaseShivaAfAutoruYandex?branch=AUTORUFRONT-16342&buildTypeTab=overview&mode=builds)

## для локальной разработки
Для того, чтобы редиректы начали работать в деве, нужно:
* запустить `www-autoru-yandex` (можно опустить, тогда запрос уйдет в тест)
* запустить `www-desktop` (он будет обрабатывать ответы от `www-autoru-yandex`)
* запустить приложение, запускающее синхронизацию в ответ на пользовательские запросы
* поменять константу `ENABLE_LOCAL_AUTORUYANDEX_APP_FOR_DEV` на `true` [тут](../auto-core/models/cookieSync/middleware/redirect-to-autoru-yandex.js)
