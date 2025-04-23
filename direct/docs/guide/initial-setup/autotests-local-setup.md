# Настройка автотестов для локальной разработки

Исходники автотестов хранятся в [Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa).
Пусть `$ARCADIA_ROOT` - локальная папка, указывающая на корень Аркадии. Тогда локально автотесты будут лежать в папке `$ARCADIA_ROOT/direct/qa`.

Для настройки автотестов нужно выполнить следующие шаги:

## 1. Настройка maven { #idea-maven }
Нужно создать папку `~/.m2` и положить туда файл `settings.xml` <https://bb.yandex-team.ru/projects/ARTFCTR/repos/settings.xml/browse/settings.xml> (ссылка [отсюда](https://wiki.yandex-team.ru/artifactory/))

## 2. Настройка IDEA для доступа в секретницу { #idea-vault-token }
Заходим в браузере на страницу [получения OAuth-токена от секретницы](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982) и копируем токен со страницы в буфер-обмена.

Открываем IDEA, заходим в меню `File -> Open` и открываем папку `$ARCADIA_ROOT/direct/qa`.

![no alt](_assets/idea-open-direct-qa.png "открываем папку $ARCADIA_ROOT/direct/qa")

Открываем в меню `Run -> Edit configurations`

![no alt](_assets/idea-run-edit-conf.png "в меню Run -> Edit configurations")

В открывшемся окне кликаем по ссылке `Edit configurations templates...`, откроется еще одно окно с шаблонами конфигураций.
Выбираем в этом окне в списке слева `JUnit` и вписываем в поле `Environment variables` строку `VAULT_TOKEN=$VAULT_TOKEN`,
где `$VAULT_TOKEN` - это токен, скопированный в буфер обмена на первом шаге.

![no alt](_assets/idea-edit-conf-defaults.png "Edit configurations templates...")

Затем нажимаем `OK` в окне `Run/Debug Configuration Templates`, и затем `OK` в окне `Run/Debug Configurations`

Дополнительную информацию можно [почитать тут](https://st.yandex-team.ru/DIRECTKNOL-9).

## 3. Выбор JDK для проектов с тестами
Сначала выбираем JDK для под которым будем работать. В правом верхнем углу IDEA, нажимаем на шестеренку и выбраем
пункт `Project Structure`.

![no alt](_assets/idea-settings-project-structure.png "Project Structure")

В открывшемся окне слева кликаем в `Project` и справа в поле `Project SDK` выбираем `JDK`. Зимой 2021 тесты успешно работали
с `JDK 11` от Яндекса, и не работали в `JDK 17`, из-за [Strongly Encapsulate JDK Internals](https://openjdk.java.net/jeps/403).

![no alt](_assets/idea-project-sdk.png "Project SDK")

## 4. Добавление корневого внутреннего сертификата в список доверенных Java { #java-add-yandex-cert }
Как и в предыдущем пункте открываем окно `Project Structure`, слева кликаем в `Project` и смотрим, какая `JDK` выбрана
справа в поле `Project SDK`.

![no alt](_assets/idea-project-sdk-selected.png "Project SDKs")

Затем, слева кликаем в `SDKs`, в середине кликаем в выбранную `JDK` и справа смотрим где она расположена.

![no alt](_assets/idea-project-sdks-yandex.png "Project SDKs")

Если в пути у папки где лежит `JDK` присутствует слово `yandex`, значит это Яндексовская JDK, и сертификат добавлять для нее не нужно.
Он уже там есть. Если же слова `yandex` в папке где лежит `JDK` нет, то сертификат придется добавлять. Для этого выделяем
и запоминаем в буфер обмена `JDK home path` из одноименного поля справа:

![no alt](_assets/idea-project-sdks-no-yandex.png "Project SDKs")

Далее действуем в зависимости от операционной системы, [согласно инструкции безопасников](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava).

## 5. Выбор и запуск тестов { #idea-add-maven }
Откройте директорию с нужными вам тестами, кликните правой кнопкой мыши по файлу `pom.xml` и в выпадающем меню
выберите пункт `Add as Maven Project`.

![no alt](_assets/idea-open-pom.png "Открыть pom-файл в IDEA")

Затем найдите нужный вам тест, кликните по нему правой кнопкой мыши и в выпадающем меню выберете пункт `Run ...` или `Debug ...`

![no alt](_assets/idea-run-test.png "Запуск теста")

## 6. Отлинковка проекта с тестами { #idea-unlink-maven }
В некоторых случаях, после добавления нескольких директорий с тестами, как проекты maven, тесты могут перестать запускаться из-за проблем с зависимостями.
В этом случае можно попробовать отлинковать ненужные в данный момент проекты с тестами. Для этого в правом верхнем углу `IDEA`
выберите закладку `Maven`, в открывшемся окне выберите ненужные проекты, кликните по ним правой кнопкой мыши и в открывшемся меню
кликните по пункту `Unlink Maven Projects`

![no alt](_assets/idea-unlink-maven.png "Unlink")

Затем в открывшемся окне нажмите на кнопку `Remove`

![no alt](_assets/idea-unlink-maven-remove.png "Remove")

## 7. Возможные проблемы
1. При запуске тестов возникает ошибка `java: error: release version 5 not supported`
   - Закройте все окна `IDEA`.
   - Проверьте, что файл `~/.m2/settings.xml` существует и его содержимое соответствует файлу <https://bb.yandex-team.ru/projects/ARTFCTR/repos/settings.xml/browse/settings.xml>.
   - Если нет, то выполните пункт [Настрока maven](#idea-maven) этой инструкции.
   - Откройте IDEA снова. Даже если файл `settings.xml` был нормальный, перезапуск `IDEA` может решить проблему.
2. Проект с тестами не хочет запускаться из-за проблем в зависимостях
   - Отлинкуйте ненужные проекты, как указано в пункте [Отлинковка проекта с тестами](#idea-unlink-maven) этой инструкции.
   - Если это не помогло, откройте `pom.xml` файл как проект Maven в отдельном окне `IDEA`.

     ![no alt](_assets/idea-open-as-maven.png "Open as project")

О других проблемах и путях их решения (например, как настроить доступ к `blackbox` с локальной машины) можно почитать в разделе [Автотесты не работают](../troubleshooting/autotests-does-not-working.md)

## 8. Дополнительные материалы

Дополнительно про настройку автотестов и работу с ними можно почитать [на вики](https://wiki.yandex-team.ru/users/upcfrost/avtotesty-direkta-posle-pereezda-v-arkadiju/#razrabotka)
 и [в тикете DIRECTKNOL-55](https://st.yandex-team.ru/DIRECTKNOL-55)
