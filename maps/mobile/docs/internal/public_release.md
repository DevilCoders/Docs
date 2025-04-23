# Как выпустить публичный релиз МапКита

#### 0. Завести тикет
[Тикет от 4.1.0](https://st.yandex-team.ru/MAPSMOBCORE-12924)

#### 1. Выбрать стабильный [релиз](https://a.yandex-team.ru/projects/maps-core-mobile-arcadia-ci/ci/releases/timeline?dir=maps%2Fmobile&id=release-all)
Релиз должен быть уже протестирован в МЯКе, в идеале раскатан на пользователей. Спросить у [@dddid777](https://staff.yandex-team.ru/dddid777)

#### 2. Запустить на нем **Release flow** `release-public` для публичного релиза. 
Во вкладке **Custom parameters** указать имя новой публичной версии (например 4.2.0) и хэш коммита предыдущего публичного релиза.

#### 3. Дождаться окончания первой `check` стадии релиза
Cгенерируется дифф idl, списка лицензий и чейнжлог с момента предыдущего публичного релиза.

#### 4. Обновить и отдать юристам список зависимостей и их лицензий
Чтобы увидеть дифф в лицензиях нажмите на Arcanum CI-бейдж задачи **Extract licenses info** на запущенном флоу.
Откроется ссылка на комит с диффом в роботной ветке.

`legal.txt` - новое содержимое этого файла в итоге нужно будет скопировать в тикет на обновление юристами [списка контрибов МапКита](https://yandex.ru/legal/maps_api/components/).
Тикет заводится в очереди [LEGAL](https://st.yandex-team.ru/LEGAL). [Тикет от 4.1.0](https://st.yandex-team.ru/LEGAL-69613)

Скорее всего, за время с предыдущего публичного релиза какие-то контрибы добавились, какие-то удалились, а какие-то обновились.
Это можно увидеть по диффу в файле `licenses.txt`. Для новых контрибов надо добавить копирайт и ссылку на лицензию в [lib_links.py](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/tools/licenses_printer/lib_links.py).
Это делается руками через поиск странички контриба в интернете. Для удаленных контрибов стоит удалить мапинг, а для обновленных проверить, что лицензия и копирайт актуальны.

Анализ и публикация списка зависимостей занимает у юристов обычно от недели минимум.
Поэтому стоит заранее их попросить быть готовыми +- к дате релиза наружу. 

#### 5. Просмотреть idl-дифф
Чтобы увидеть дифф в .idl файлах нажмите на Arcanum CI-бейдж задачи `Make idl diff` на запущенном флоу.
Откроется ссылка на комит с диффом в роботной ветке.

Стоит пробежаться по диффу, проверив, например, не забыты ли `@undocumented` и `@internal` поля в новом коде. Есть ли комментарии у новых сущностей. 

#### 6. Составить сhangelog
В будущем в CI публичного релиза должна быть таска по сбору changeloga.
Она и опрос в тикете руководителей групп (рендеринга, навигации, итд) должна помочь собрать крупноблочный и человеко-ориентированный [changelog для новых версий](https://yandex.ru/dev/maps/mapkit/doc/dg/concepts/versions.html).

#### 7. Разблокировать `build` стадию релиза
Соберутся full и lite мапкиты, документация и mapkit-demo приложения.

#### 8. Обновить [русскую документацию](https://yandex.ru/dev/maps/mapkit/doc/intro/concepts/about.html) и [английскую документацию](https://yandex.com/dev/maps/mapkit/doc/intro/concepts/about.html)
Просмотреть на quickstart инструкции под [android](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/docs/mapkit/quickstart_android.md) и [ios](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/docs/mapkit/quickstart_ios.md)
Как минимум обновить версию в примерах. В случае правок текста, стоит пригласить в ревьюшку [@egilmanova](https://staff.yandex-team.ru/egilmanova).

Завести тикет в [DOC](https://st.yandex-team.ru/DOC) на [@egilmanova](https://staff.yandex-team.ru/egilmanova) на обновление документации. В тикете нужно дать ссылку на:
* Quickstart инструкции под [android](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/docs/mapkit/quickstart_android.md) и [ios](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/docs/mapkit/quickstart_ios.md)
* Крупноблочный и человеко-ориентированный чейнжлог из [пункта 6](#6-Составить-сhangelog)
* Автоматическая документация (справочник) из ресурсов, собранных в запущенном флоу в 4х sandbox тасках `Release full/lite android/ios docs`

Также нужно запросить в тикете английский перевод для английской документации. В целом время согласования документации несколько дней, для перевода может потребоваться до недели.  

[Тикет от 4.1.0](https://st.yandex-team.ru/DOC-9554)

#### 9. Протестировать MapkitDemo
Нужно дать ссылки [@dddid777](https://staff.yandex-team.ru/dddid777) для тестирования на собранные в запущенном флоу в 2х sandbox тасках `Build MapKitDemo App for android/ios` приложения.

#### 10. Разблокировать `export` стадию
Мапкиты зальются в публично доступные mds-бакеты и maven-репозитории.

#### 11. Выложить Podspec
Зайти из флоу в sandbox задачу `Release full ios mapkit` и скачать к себе `POD_SPEC` ресурс, как `YandexMapsMobile.podspec`.
Запустить команду `pod trunk push YandexMapsMobile.podspec`.

Повторить эту же процедуру для `Release lite ios mapkit`.

Новые podspecs должны появиться в [репозитории](https://github.com/CocoaPods/Specs/tree/master/Specs/d/d/0/YandexMapsMobile)

Если вы не в списке `Owners` пода (`pod trunk info YandexMapsMobile`), [зарегистрируйтесь и попросите овнера вас добавить](https://guides.cocoapods.org/making/getting-setup-with-trunk.html). 

#### 12. Подтвердить экспорт в maven-репозитории
Залогиниться в [Nexus repository manager](https://oss.sonatype.org/#welcome) c [логин-паролем](https://yav.yandex-team.ru/secret/sec-01g3fcndbhtwmvrpwhff69k6k1/explore/versions).
Выбрать в `Staging Repositories` свои реквест(ы) и нажать кнопку `Close`. После выбрать свои реквест(ы) и нажать кнопку `Release`. После `Release` доезжает в [Maven Central](https://search.maven.org/artifact/com.yandex.android/maps.mobile) за десятки минут.

{% note warning %}

Это логин-пароли для публикации всех мобильных библиотек Яндекса, в списке реквестов вы можете увидеть не только МапКит.

{% endnote %}

#### 13. Обновить версии МапКита в MapkitDemo и выложить на github
Обновить версии под android в [build.gradle](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/apps/mapkit_demo/android/build.gradle) и ios [Podfile](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/apps/mapkit_demo/ios/Podfile), [Podfile.lock](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/apps/mapkit_demo/ios/Podfile.lock).
Проверить локально, что собирается и работает (для этого надо еще api_key прописать).
Сделать пулл реквесты (без api_key) с обновлением в [ios](https://github.com/yandex/mapkit-ios-demo) и [android](https://github.com/yandex/mapkit-android-demo). Попросить коллегу с доступом ([@trivias](https://staff.yandex-team.ru/trivias)) вмерджить пулл-реквест. 

Отписаться в необходимых issues на github о пофикшенах багах в новой версии.

Для консистентности можно обновить [конфиг и Podspec файлы](https://a.yandex-team.ru/svn/trunk/arcadia/maps/mobile/ci/tsr/apps/mapkit_demo/ios), необходимые для хака со сборкой с подкладыванием локального артефакта в CI. 

#### 14. Проконтролировать обновление внешних страниц:
Проверить, что сошлись задачи на обновления:
* [Информация о стороннем программном обеспечении в составе SDK для сервиса «Яндекс.Карты»](https://yandex.ru/legal/maps_api/components).
* Документации:
  * [Android Начало работы](https://yandex.ru/dev/maps/mapkit/doc/android-quickstart/concepts/android/quickstart.html)
  * Android Справочник lite версии
  * Android Справочник full версии
  * [iOS Начало работы](https://yandex.ru/dev/maps/mapkit/doc/ios-quickstart/concepts/ios/quickstart.html)  
  * iOS Справочник lite версии
  * iOS Справочник full версии
  * [Версии MapKit](https://yandex.ru/dev/maps/mapkit/doc/dg/concepts/versions.html)  
* Английской документации:
  * [Android Getting started](https://yandex.com/dev/maps/mapkit/doc/android-quickstart/concepts/android/quickstart.html)
  * Android Lite version reference
  * Android Full version reference
  * [iOS Getting started](https://yandex.com/dev/maps/mapkit/doc/ios-quickstart/concepts/ios/quickstart.html)
  * iOS Lite version reference
  * iOS Full version reference
  * [MapKit SDK Versions](https://yandex.com/dev/maps/mapkit/doc/dg/concepts/versions.html)
* Новая документация проиндексирована, а старая удалена из индексации. Поиск на странице документации показывает новые версии. 
* Правильность ссылок на [лендинг странице](https://yandex.ru/dev/maps/mapkit/#examples) и [английской версии](https://yandex.com/dev/maps/mapkit/#examples). Если необходимы изменения, создать тикет в [TECHCONTENT](https://st.yandex-team.ru/TECHCONTENT). [Тикет от 4.1.0](https://st.yandex-team.ru/TECHCONTENT-424)

#### 15. Разблокировать последнюю задачу во флоу `Save commit number in arcadia` по обновлению коммита последнего публичного релиза.
По CI-бейджу перейти в созданную ревьюшку и вмерджить ее.
