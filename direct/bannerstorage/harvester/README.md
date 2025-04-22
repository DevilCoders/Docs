# bannerstorage-harvester
Сервис по обработке асинхроных событий BannerStorage'а

# Генерация проекта для IntelliJ IDEA (пример)
```
find . -name ya.make | xargs grep -lE 'JAVA_PROGRAM|JAVA_LIBRARY|JTEST|JUNIT5' | perl -pe 's/\/ya.make//; s/^/-C /' | xargs ya ide idea -DJDK_VERSION=11 --local --iml-in-project-root -r "/home/${USER}/proj/idea-project-bannerstorage" -j12 --stat --group-modules=tree
```
# Сборка докер-контейнера через ya make (пример)

Убедитесь, что у вас есть роль contributor в docker registry медийки:

[Ссылка на роль в IDM](https://idm.yandex-team.ru/system/docker/roles#f-status=all,f-role=docker/distribution_prefix/mediaselling%7C/contributor,sort-by=-updated,f-is-expanded=true,f-state=granted)

если роли нет, то запросите. Далее можно выполнить команду для сборки образа и загрузки его в docker registry

```
ya package package/package.json --docker --docker-repository mediaselling --custom-version 000001-test --docker-push
```

В качестве версии стоит указывать номер вида 260-f4acd3e, где 260 -- порядковый номер сборки (текущий номер можно посмотреть в Деплое), а суффикс -- короткий хеш текущей ревизии

Документация к команде сборки [https://docs.yandex-team.ru/devtools/package/docker](https://docs.yandex-team.ru/devtools/package/docker)

# Запуск собранного докер-контейнера локально (пример)
```
# в файл env-vars нужно поместить переменные окружения
docker run -i --env-file=env-vars --network mynetwork registry.yandex.net/mediaselling/harvester:000001-test
```

# Wiki
https://wiki.yandex-team.ru/bannerstorage/harvester/

# Запуск
На данный момент поддерживаются три Spring-овских profile-я: default (ничего не указывать), production, testing. По умолчанию сервис слушает порт 8080.
Основные параметры запуска расположены в файлах application.properties (глобальный значение параметров) и application-(production|testing).properties
profile специфичные параметры. Также на Spring-овских profile-х построено включение обработчиков очередей. На данный момент поддерживаются
следующие profile-и для очередей:
 * screenshots (Очередь для обработки screenshot-ов, dbo.NotifyCreativePredeployServiceQueue)
 * process_dynamic_codes (Очередь для обработки JS-обвязок, dbo.CreativeProcessDynamicCodeServiceQueue)
 * automoderation (Очереди для интеграции с автомодерацией, dbo.AutoModerationStartServiceQueue, dbo.AutoModerationPollServiceQueue, dbo.AutoModerationWaitServiceQueue)
 * rtb_creative_changed (Очередь для уведомления БК о изменении в креативе, dbo.RtbHostLinkCreativeChangedServiceQueue)
 * rtb_postmoderation (Очереди для выгрузки из БК offer-ов на модерацию или отправки назад отмодерированных, PostModeration.RecvModeratedOffersQueue, PostModeration.SendModeratedOffersQueue)
 * ssl_insecure (Профиль для отключения проверки SSL-сертификатов, чтобы можно было пользоваться в разработческой среде, в стоковой JDK)

Параметры запуска:

|Параметр|Описание|
|--------|--------|
|ENVIRONMENT_TYPE *|Тип среды, в которой запускается контейнер (Возможные значения production и testing)|
|ACTIVE_QUEUES *|Список активных очередей, через запятую (Возможные значения screenshots, process_dynamic_codes, rtb_host и automoderation). Хотя бы одно должно быть указано|
|SENTRY_DSN *|Url sentry, в который будут логироваться ошибки|
|BANNERSTORAGE_DB_URL *|JDBC Url подключения к базе данных BannerStorage|
|BANNERSTORAGE_DB_USERNAME *|Имя пользователя, под которым будет ходить сервис|
|BANNERSTORAGE_DB_PASSWORD *|Пароль пользователя, под которым будет ходить сервис|
|SCREENSHOT_URL|Url для получения превью креатива, например http://media-adv-screenshoot.haze.yandex.net/screenshots. Обязателен если включена очередь screenshots|
|AVATARNICA_READURL|Url для чтения из аватарницы, например http://avatars.mdst.yandex.net/ (cм. https://wiki.yandex-team.ru/mds/avatars/)|
|AVATARNICA_WRITEURL|Url для записи в аватарницу, например http://avatars-int.mdst.yandex.net:13000/ (см. https://wiki.yandex-team.ru/mds/avatars/)|
|AVATARNICA_NAMESPACE|Namespace в аватарнице, например bstor (cм. https://wiki.yandex-team.ru/mds/avatars/)'|
|PHANTOMJS_SERVICE_URL|URL сервиса проверки Phantom JS, например, https://automoderation-phantomjs-api.mediaselling.yandex.net|
|RTBHOST_URL|Url к RTB хосту, например http://bssoap.yandex.ru/export|
|PASSPORT_URL *|Url Яндекс-паспорта, например https://passport.yandex-team.ru/|
|VIRUSTOTAL_URL *|Url proxy VirusTotal-а, например https://virustotal.viewer.yandex-team.ru/|
|VIRUSTOTAL_ROBOTLOGIN *|Яндекс-паспорт логина робота под которым будем ходить в proxy VirusTotal-а|
|VIRUSTOTAL_ROBOTPASSWORD *|Яндекс-паспорт пароль робота под которым будем ходить в proxy VirusTotal-а|
|PREMODERATION_URL *|Url интерфейса премодерации без завершающего слеша, например, https://premoderation.mediaselling.yandex.net|

\* - обязательные параметры

По умолчанию контейнер mount-ит папку /tmp хоста
