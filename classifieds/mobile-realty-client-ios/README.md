Яндекс Недвижимость для iOS
========================

## Начало
1. Для установки и настройки аркадии воспользуйтесь [инструкцией](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

2. После того, как Аркадия была смонтирована перейдите в папку проекта:
`<путь до arc>/classifieds/mobile-realty-client-ios`

3. Перед первым запуском проекта необходимо установить [Ruby, Bundler, rvm](https://wiki.yandex-team.ru/realty/mobile/ios/Realty-Library-Dependencies/).

4. Для работы подов нужно выполнить команду 
`export POD_GEM_PATH=../mobile-cocoapods-tools`
   
5. После этого выполнить (а также делать после каждой смены веток) `./realty pod install` (либо `bundle exec pod install`).

6. Если все предыдущие шаги выполнены успешно, можно открывать `YandexRealty.xcworkspace` и запускать проект.  

## Инструменты

`Xcode` - **13.x**

`Cocoapods` (см. файл `Gemfile`)

`Ruby` (см. файл `.ruby-version`)

## Важно
Прежде чем вносить свой вклад в проект, ознакомься, пожалуйста, с [Wiki](https://wiki.yandex-team.ru/realty/mobile/ios/). Ответы на большинство вопросов (код-стайл, архитектура, как работать с проектом и т.д.) ты сможешь найти там. 

## Тулза Realty
[Инструмент](https://wiki.yandex-team.ru/realty/mobile/ios/instruments/#realty-tool) для автоматизации рутинных задач. Включает в себя специальный **генератор модулей и пакетов**. 

## [How To & Best Practices](https://wiki.yandex-team.ru/realty/mobile/ios/HowToandBestPractices/)

## [Репозиторий билд-скрипта](https://a.yandex-team.ru/arcadia/classifieds/mobile-realty-client-ios-buildscript)
