# Исходный код регистрационной анкеты ПИ2

## Как запустить локальную версию этого проекта

 1. Нужно поставить nginx и docker
 2. В файл `/etc/hosts` на своем компьютере вписать строку `127.0.0.1 localhost.yandex.ru`
 3. Склонировать этот репозиторий
 3. В папке с кодом из этого репозитория запустить `./restart`
 4. Дождаться пока все собереться (в первый раз это выполняется долго)
 5. После того как все собереться нужно зайти на https://localhost.yandex.ru
    * по адресу https://localhost.yandex.ru/swagger/ располагается Swagger с описанием всех ручек
    * по адресу https://localhost.yandex.ru/form/ располагается обычная анкета РСЯ
    * по адресу https://localhost.yandex.ru/form/mobile_mediation/ располагается анкета Мобильной Медиации
    * по адресу https://localhost.yandex.ru/form/video_blogger/ располагается анкета Видео-Блогеров
    * по адресу https://localhost.yandex.ru/form/games/ располагается анкета для Игр
    * по адресу https://localhost.yandex.ru/form/assessor/ располагается анкета для асессоров
    * по адресу https://localhost.yandex.ru/form/efir_blogger/ располагается анкета Блогеров Эфира

## Как заполнить форму повторно
1. Если нужно почитисть данные только в базе ПИ (cм [вики](https://wiki.yandex-team.ru/partner/w/partner2-intapi-form-rm-user-in-db/))
```
curl 'https://partner2-test.yandex.ru/intapi/form/rm_user_in_db.json?user_id=607369863'; echo
{"data":"ok","result":"ok"}
```
2. Если нужно полностью удалить пользователя и в ПИ, и в балансе, надо выполнить команду
```
./delete [UID]
```
(дефолтный UID = 607369863, то есть обычно можно вызывать без параметров)

или выполнить напрямую ту команду, которую она вызывает:
```
docker exec -it form_api_1 carton exec -- perl -Ilib -It_lib bin/submit.pl --uid=607369863 --delete
```
Если выдала список sql-команд, значит какие-то проблемы с БД и надо или повторить вызов, или выполнить их вручную в БД.

## Как переключить локальную версию проекта на бету

По умолчанию этот проект взаимодействует с https://partner2-test.yandex.ru

Для того чтобы переключить его на какую-нубудь бету нужно вписать адрес этой беты в файл `external_nginx/nginx.conf`:

```diff
--- a/external_nginx/nginx.conf
+++ b/external_nginx/nginx.conf
         location / {
-            proxy_pass https://partner2-test.yandex.ru;
+            proxy_pass https://dev-partner.yandex.ru:8466;
         }
```

И после этого сделать `./restart`.

## Как собрать и выложить релиз — backend

 1. Проверить что другие люди не собирают релиз анкеты
 1. Замержить задачу (или задачи) в master
 1. Переключить рабочую копию на текущий master
 1. Перезапустить систему `./restart`
 1. Прогнать тесты `./check` — все тесты должны быть зеленые
 1. Поправить файл `./build` — раскомментировать и указать значение для VERSION. Значение — это текущая дата, плюс номер сборки за этот день (смотреть в deploy какие уже были)
 1. В файле `./build` закомментировать строку `cd lordran; ...` (мы выкладываем backend, для выкладки backend не нужно собирать фронт)
 1. Запустить `./build` — он соберет докерный образ
 1. Выполнить команду которую выдал `./build` (Команда `docker push registry.yandex.net/partners/form_api:$VERSION"` в которой вместо `$VERSION` находится настоящая версия) — это зальет образ в общеяндексовый регистри
 1. Выложить образ в тестовое окружение deploy — https://deploy.yandex-team.ru/stages/form-test
 1. Проверить работу анкеты на ТС https://partner2-test.yandex.ru/form/
 1. Выложить образ в препрод окружение deploy — https://deploy.yandex-team.ru/stages/form-preprod
 1. Проверить работу анкеты на препроде https://partner2-preprod.yandex.ru/form/
 1. Если все ок, то выложить образ в прод окружение deploy - https://deploy.yandex-team.ru/stages/form-prod

## Как собрать и выложить релиз — frontend
смотри [lordran/README.md](lordran/README.md#Как-собрать-и-выложить-релиз--frontend)

## Просмотр логов STDERR

### Dev

```
docker logs -f --tail 50 form_api_1
```

### Prod, Test

1. Логи c последнего релиза можно поглядеть через UI deploy во вкладке логов

2. Более старые логи можно найти в YT одним из запросов:
- Универсально, но долго (5-10 мин):
```
SELECT * FROM arnold.`logs/deploy-logs/1d/<ДАТА ПРИМЕР: 2021-01-22>` WHERE stage='form-test' LIMIT 1;
https://yql.yandex-team.ru/Operations/YCT0EAPTTmFAbvn3mlB4Sw8QUWxK8KBP8fhm0RchRtU=

```

## FAQ

### Зачем нужен `external_nginx`?
Чтобы локальная анкета нормально работала с ipv6only машинами.
[Эту проблему за 2,5 года так и не починили](https://github.com/docker/for-mac/issues/1432#issuecomment-511215929), так что надеяться уже не приходится.
Вообще, докер работает по-разному под разными ОС. Для каждой нужен свой набор костылей.
Поэтому, кажется, правильно переехать на какой-нибудь дев-сервер и поддерживать 1 набор костылей.
Или запускать анкету не в докере, а в каком-нибудь яндексовом облаке, где проблем с ipv6only нет. В адфоксе так делают, и вроде норм.


### Как обновить переводы
При прогоне тестов новые ключи добавляются в `translations/ru.json`.
Проверить, есть ли ключи на переводы:
```
diff <(jq 'keys' api/translations/en.json) <(jq 'keys' api/translations/ru.json)
6a7
>   "Асессор",
64a66
>   "Канал",
77a80
>   "Название банка получателя. Например, ЗАО Альфа-банк",
104a108
>   "Пустой логин или пароль",
115a120,121
>   "Ссылка на ваш канал",
>   "Ссылка на канал в формате https://www.youtube.com/channel/name",
141a148
>   "Указанный SWIFT не найден",
```

Загрузить ключи в танкер можно скриптом (надо взять токен из секретницы и прописать его в $ENV{TOKEN}):
`bin/upload_translations_to_tanker`

После этого нужно создать тикет на переводчиков скриптом из ПИ, подпатчив его подобным образом:
```
diff --git a/bin/create_startrek_ticket_for_translators.pl b/bin/create_startrek_ticket_for_translators.pl
index 198759f316..f310a45e21 100755
--- a/bin/create_startrek_ticket_for_translators.pl
+++ b/bin/create_startrek_ticket_for_translators.pl
@@ -92,15 +92,22 @@ sub get_translations_from_tanker {
     my $keysets = from_json(Encode::decode_utf8($tanker->get_project_tjson(status => 'unapproved')))->{'keysets'};
     my %tickets = map {$_ => 1} @{$opts->{tickets}};

+    my @s = (
+        "Асессор",
+        "Канал",
+        "Название банка получателя. Например, ЗАО Альфа-банк",
+        "Пустой логин или пароль",
+        "Ссылка на ваш канал",
+        "Ссылка на канал в формате https://www.youtube.com/channel/name",
+        "Указанный SWIFT не найден",
+    );
+    my %h = map { $_ => 1 } @s;
+
     print "Finding translations\n" unless $opts->{json};
     my $result = {};
-    foreach my $keyset (keys(%$keysets)) {
-        foreach my $key (keys(%{$keysets->{$keyset}{'keys'}})) {
-            my $ticket_context = $keysets->{$keyset}->{'keys'}->{$key}->{'info'}->{'context'};
-            my ($ticket, $context_with_space, $context) =
-              ($ticket_context // '') =~ /^$startrek_base_url([A-Za-z]{2,}-\d+)( (.*))?$/;
-
-            if ($ticket and $tickets{$ticket}) {
+    foreach my $keyset (qw(form)) {
+        foreach my $key (@s) {
+            if ($h{$key}) {
                 $result->{$keyset}->{$key} = 1;
             }
         }
```
Проверить, что попадает в тикет:
```
/bin/create_startrek_ticket_for_translators.pl --tickets=PI-20644 --tanker-project=pi2 --dry-run
```

GZ!

## Обновить сертификат
Если протух сертификат, нужно выписать новый в https://crt.yandex-team.ru/ -> Заказать сертификат

Поля
CA name    -> InternalCA
TTL        -> 365
Хосты      -> localhost.yandex.ru
ABC-сервис -> Партнёрский интерфейс РСЯ

Жмём "Заказать" и новый сертификат подкладываем вместо nginx/localhost.yandex.ru.pem
