# Arcadia Native Code 4 Android

В этой папке лежат запчасти, которые нужны для удобной поставки нативного кода из Аркадии в
Android-приложения.

## Общая схема

Рядом с нативным кодом в Аркадии кладётся описание [пакета](https://wiki.yandex-team.ru/yatool/package/).
С помощью скрипта `deploy.py` в этой папке на Sandbox запускается сборка этого пакета, затем
результат сборки в виде AAR заливается в Artifactory, откуда его уже можно классическим образом использовать,
прописав зависимость в gradle.

## Пример запуска

`./deploy.py --package "search/mobile/android/package.json" -r 7304002 -s settings.xml`

Здесь указывается путь к пакету от корня Аркадии, ревизия и путь к файлу с настройками публикации
(канонические настройки есть в этой же папке).

Вместо `-r` можно указать `-b <полное имя users/ ветки>` или `-b <hash коммита>`.

## Тонкости

Чтобы всё хорошо работало, имя пакета должно представлять из себя `groupId:artifactId`, версия
пакета, соответственно, тоже должна быть адекватная (она используется как версия артефакта).

Для отладки (при разработке нативной библиотеки) её стоит собирать локально штатными средствами
(с помощью запуска `ya package`) и затем подкладывать прямо `.aar`-файл в gradle-сборку
(см. https://appmediation.com/how-to-add-local-libraries-to-gradle/).

Также в необходимо добавить переменную `ARC_TOKEN` в Vault Sandbox'a со своим токеном (из файла `~/.arc/token`).

Если при запуске получаете ошибку
```
HTTPError: (u'400 Client Error: BAD REQUEST for url: https://sandbox.yandex-team.ru/api/v1.0/task',): {"reason": "User \"guest\" does not belong to the group \"<ваш логин>\""}
```
то нужно указать в переменной окружения `SANDBOX_TOKEN` ваш [OAuth токен](https://sandbox.yandex-team.ru/oauth) к Sandbox api.

## Где уже используется

Лучше всего, конечно же, посмотреть примеры пакетов:

 * [единый артефакт Аркадии для ПП](https://a.yandex-team.ru/arc/trunk/arcadia/search/mobile/android/package.json)
 * [единый артефакт Аркадии для Бро](https://a.yandex-team.ru/arc/trunk/arcadia/search/mobile/android/package-bro.json)
 * [библиотека офлайн-поиска](https://a.yandex-team.ru/arc/trunk/arcadia/quality/trailer/offline_search/android/package.json)
 * [нативная либа Я.Клавиатуры](https://a.yandex-team.ru/arc/trunk/arcadia/keyboard/android/native/aar/package.json)
 * [нативная либа Я.Переводчика](https://a.yandex-team.ru/arc/trunk/arcadia/dict/mt/libs/mobile/android/package.json)

Если будут вопросы, приходите к dvorkanton@.
