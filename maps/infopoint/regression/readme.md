# Подготовка списка тестовых пользователей для стрельб
При работе с разными видами черного ящика для авторизации пользователя требуется передать его валидный OAuth токен. Список пользователей для стрельбы указывается в отдельном файле, где на каждой строчке через пробел указаны uid и OAuth токен пользователя. При генерации патронов через requestgen путь к файлу со списком указывается через параметр -u (--users). Готовый файл со списком пользователей и их токенами можно скачать тут: [user_tokens](https://yav.yandex-team.ru/secret/sec-01f8fr0m1s1g4bzqxvrv4z3kde). Токены живут один год. Если они протухнут, потребуется скачать учетные данные тестовых пользователей [user_credentials](https://yav.yandex-team.ru/secret/sec-01f8fr0m1s1g4bzqxvrv4z3kde) и воспользоваться утилитой [generate_tokens](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/regression/users-generator).

# Генерация патронов по логам NGINX
## 1. Сгенерировать файл logstat
Для создания патронов требуется генерация промежуточного файла - logstat. Он не привязан к чему-либо и не может испортиться. Для создания logstat подайте скрипту [logstat](https://a.yandex-team.ru/arc_vcs/maps/infopoint/regression/logstat) файл с access-tskv логом nginx в stdin. Скрипт отдаст результат своей работы в stdout. Пример использования:
```
cat /var/log/nginx/access-tskv.log | ./logstat > logstat_file
```
## 2. Сгенерировать патроны
[Генератор патронов](https://a.yandex-team.ru/arc_vcs/maps/infopoint/regression/requestgen) имеет несколько аргументов. В качестве параметра -c (--conf) укажите конфиг-файл, например [config.json](https://a.yandex-team.ru/arc_vcs/maps/infopoint/regression/requestgen/config.json). В аргументе параметра -s (--stat) укажите путь к файлу logstat. В опциональном аргументе -u (--users) укажите файл со списком авторизованных пользователей. Пример использования:
```
./requestgen -c config.json -s logstat_file -u users
```
Результат из stdout скрипта можно записывать в файл и заливать в лунапарк.<br>
Генератор патронов в качестве первых N патронов генерирует запросы добавления X точек и Y комментариев, где N = X + Y (патроны преднаполнения базы данных). Параметры X и Y описываются в config.json в секции `INIT_COMMANDS`. Эти точки и комментарии потом используются для стрельбы, чтобы выполнять такие запросы, как получение и модерация точек и комментариев (выполнять такие запросы на пустой базе в стрельбах, очевидно, не имеет смысла). Числа X и Y должны быть подобраны таким образом, чтобы размер базы соответствовал таковому в stable окружении. Именно поэтому в каждом сценарии стрельбы первой фазой идет фаза наполнения базы: константая стрельба продолжительности T с рпс RPS такими, что T * RPS = N. А чтобы база не росла бесконечно, после каждой стрельбы она очищается (см. ниже).<br>
При генерации патронов по logstat'у игнорируются (не добавляются в патроны) запросы, поступающие от tie-events и старой мобильной прокси, так как это тяжелые запросы, частота которых не зависит от нагрузки, создаваемой пользователями. Добавление этих патронов сильно искажает профиль стрельбы, подробнее смотри в [MAPSCORE-4816](https://st.yandex-team.ru/MAPSCORE-4816).<br>
Результат из stdout скрипта можно записывать в файл и заливать в лунапарк.
# Генерация GDPR патронов
## Сгенерировать патроны для наполнения контента.
- Перейти в раздел [generation](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/regression/generation)
- Взять, сгенерированный из access-tskv лога, logstat_file
- Сгенирировать патроны
```sh
cat logstat_file | ./generate_content_logstat.py > gdpr_content_logstat

./requestgen -c config_no_prefill.json -s gdpr_content_logstat -u users > gdpr_content_ammo
```
## Сгенерировать gdpr патроны
- Перейти в раздел [generation](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/regression/generation)
- Сгенирировать патроны
```sh
./generate_gdpr_logstat.py > gdpr_logstat

./requestgen -c config_no_prefill.json -s gdpr_logstat -u users > gdpr_ammo
```

## Сгенерировать sq2 патроны
- Перейти в раздел [generation](https://arcanum.yandex-team.ru/arc/trunk/arcadia/maps/infopoint/regression/generation)
- Сгенирировать патроны
```sh
./generate_sq2_logstat.py > sq2_logstat

./requestgen -c config_no_prefill.json -s sq2_logstat -u users > sq2_ammo
```

# Очистка базы
Выполняется дерганием ручки `/wipe_data`, при этом полностью очищаются коллекции `points` и `users`.
# Как залить патроны
Залить как sandbox ресурс:<br>
`ya upload ammo.txt --ttl inf -d 'Infopoints ammo'`<br>
Используя api лунапарка:<br>
`curl https://lunapark.yandex-team.ru/api/addammo.json -F'login=YOUR_LOGIN' -F'dsc=SOME_DESCRIPTION-0' -F'file=@ammo.txt'`<br>
В ответе будет ссылка на залитые в mds патроны.
