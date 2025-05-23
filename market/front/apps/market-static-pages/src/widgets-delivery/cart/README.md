# Демонстрационный лендинг корзинного виджета Доставки

## Ответственные за пакет

-   Сервис в ABC - https://abc.yandex-team.ru/services/market-affiliate
-   Рассылка - marketaffiliate@yandex-team.ru
-   Телеграмм - https://t.me/joinchat/C-B5WUWGZrcpYxBrvnudQw

## Сборка проекта

`npm run dev` - Стартует сервер на порте 1234 запускает watch режим, отслеживает изменения исходных файлов

`npm run release` - Сборка релизной версии для выкладки

PS: Рекомендуемая для сборки версия nodejs 10.6.0

## Как сделать и выкатить изменения

1. Клонируем репозиторий https://github.yandex-team.ru/market/market-static-pages
2. Переходим в папку с исходниками нашего сайта - https://github.yandex-team.ru/market/market-static-pages/tree/master/src/widgets-delivery/cart/
3. Устанавливаем зависимости - `npm install`
4. Отводим ветку от мастера. Делаем коммит с изменениями. Для разработки используем сборку через команду `npm run dev`
5. Чтобы изменения в исходниках применились на сайте в проде, нужно пересобрать и выложить release-версию кода. Для сборки выполняем команду `npm run release`. В папке `public` появятся измененные файлы - добавляем их в тот же коммит или в отдельный.
6. Пушим изменения. Создаём `pull request`. Проходим ревью. При внесении правок в код исходников не забываем пересобирать релизную версию.
7. После того, как ревью пройдено, мержим код в `master`.
8. Чтобы выложить release-версию в прод, клонируем sandbox таску BUILD_MARKET_FRONT_STATIC ([ссылка](https://sandbox.yandex-team.ru/task/82694341/view))
9. В конфиге меняем описание и номер тикета в стартреке. Проверяем, что указана ветка `master`. Запускаем таску (кнопка `Run`).
10. После того, как таска выполнится, у неё слева от `Clone` появится кнопка `Release`. Жмём её, из выпадающего списка выбираем `stable`, остальные поля можно оставить пустыми, подтверждаем релиз.
11. Через некоторое время изменения окажутся в проде.

## Как собрать тестинг

Адрес тестинга - https://market-static-pages.tst.vs.market.yandex.net/widgets-delivery/cart/

Перед тем, как мержить изменения в `master` и релизить в прод, можно их проверить в тестинге. После того, как изменения запушены на удаленную ветку, можно выполнить шаги по публикации кода с помощью sandbox таски. Только при клонировании таски вместо ветки `master` указать фича-ветку с изменениями, а при релизе вместо `stable` выбрать `testing`.
