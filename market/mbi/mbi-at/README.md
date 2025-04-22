## Подготовка приложения к сборке

Необходимо скопировать [файл](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi-tools/maven/settings.xml)
в `~/.m2/settings.xml`

Альтернативным вариантом является запуск [скрипта](https://github.yandex-team.ru/market-java/mbi-at/blob/master/setup-maven-settings.sh),
который качает `settings.xml`

## Сборка приложения

**Внимание!**<br>
Приложение (временно) не получится собрать 11й джавой, поэтому необходимо переопределить `JAVA_HOME` для сессии терминала:
```
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_202.jdk/Contents/Home
```

Первая сборка:

```
mvn clean install
```

В дальнейшем, если будет падать
```
mvn clean install
```
то выполняем
```
mvn clean package
```

Профили maven:
```
production, testing - окружение aqua
upload-aqua         - при активации - загружать собранную версию в aqua
```
Для локальной разработки деплой артефактов стоит отключать чтобы не перезаписывать имеющиеся версии.
Это можно сделать отключив профиль `upload-aqua`: `mvn install -P '!upload-aqua'` или в меню `maven -> profiles` в IntelliJ IDEA.

## Локальный запуск тестов

Если тесты падают с ошибкой **403**, то необходимо [пропатчить](https://wiki.yandex-team.ru/users/luba239/notes/java/patch/)
джаву.

### Запуск тестов с секретами.
1) Получить токен для [Секретницы](https://yav.yandex-team.ru) по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
2) Выставить переменную окружения `VAULT_TOKEN`, равную полученному токену.
3) Убедиться, что есть доступ к секрету из `ru.yandex.autotests.market.mbi.environment.MbiSecrets.VAULT_HEAD_ID` - [секрет](https://yav.yandex-team.ru/secret/sec-01ctnx7n3ss4pbmcvex94evaaa)

## Релизы приложения

Находясь в Аркадии, приложение по-прежнему релизится через Teamcity.<br>
Новая версия автоматически подхватывается после мержа в транк, дополнительных действий не требуется.<br>
Следить за релизом можно в [таске](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Mbi_Deploy_MbiAtArcadiaBuild).

Прекоммитная сборка отсутствует, поэтому необходимо перед мержем собрать проект локально.

##
[Дополнительная информация о секретнице.](https://clubs.at.yandex-team.ru/life-of-qa/537)
