# readme

# ![Icon](./AutoRu/Resources/Assets.xcassets/AutoRu-AppIcon.appiconset/120.png =40x40) iOS клиент Auto.ru

### Главное

Для работы над проектом используйте AutoRu.xcworkspace

### ARC

Проект лежит в Аркадии по пути 

```bash
/arcadia/classifieds/mobile-autoru-client-ios/
```

Инструкция по настройке Аркадии 

[https://docs.yandex-team.ru/devtools/intro/quick-start-guide](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

### Конфигурация приложения

Для того, чтобы поменять настройки приложения, нужно использовать отдельное приложение `QA Assist`. Поставить можно из канала со сборками (в закрепе или поискав QAssist) по [ссылке](https://t.me/joinchat/RkzvJLkZnmsdRkup)

Код приложения лежит в [/utils/mobile-autoru-client-settings-ios] для сборки на симуляторе просто запустить в xcode предварительно сделав в этой директории pod install

### Бэкенд

Список доступных ручек можно посмотреть в [swagger](http://autoru-api-server.vrts-slb.test.vertis.yandex.net/swagger/?url=/api-docs#!/)

Очередь [AUTORUAPI](http://st.yandex-team.ru/AUTORUAPI)

Формат сообщений для комуникации с бэкендом описан через [protobuf](https://developers.google.com/protocol-buffers/). Файлы с описание лежат в репозитории [schema-registry](https://a.yandex-team.ru/arcadia/classifieds/schema-registry). На основе этих файлов создаются файлы на Swift.

Чтобы сгенерировать новые модели необходимо добавить название корневых классов в /Tools/Sources/RootProtomodels

После чего запустить схему ProtoGenerator в xcode

### Тесты

Чтобы сгенерировать таргет с UITest необходимо запустить схему UITestProjectGenerator в xcode

Как пишем тесты описано в [wiki](https://wiki.yandex-team.ru/vsapps/autoru-mobile/ios/how-to-write-tests/)

### Swift formatter

Чтобы отформатировать файлы, которые ты правил в ветке, запусти схему SwiftFormatter в xcode

### Доп инфа

[ботик для уведомлений из аркадии](https://t.me/ya_arcanum_bot)

Вики [AutoRu](https://wiki.yandex-team.ru/vsapps/autoru-mobile/)

[Наш трекер задач](https://st.yandex-team.ru/)

Дока по SSR в отчетах (coming soon)

[Как сделать новый релиз](https://wiki.yandex-team.ru/autoru-mobile/ios/how_to_release/)

[Дока AutoRu](https://docs.yandex-team.ru/autoru-ios/)
