# business_analytics_cron

Здесь лежат все скрипты, которые запускаются для бизнес-аналитики Такси. Все скрипты запускаются из под профиля [robot-taxi-business](https://staff.yandex-team.ru/robot-taxi-business) на машинке analytics-cron-sas-01.taxi.tst.yandex.net

Отбивки о работе скриптов робот присылает на рассылку taxi-analyst-cron@yandex-team.ru. Если хотите персонализированные нотификации, [почитайте про Handler](https://github.yandex-team.ru/rotax/business_models/blob/develop/common_scripts/Handler.ipynb).

Для работы с гуглдоком выдавайте доступ роботу robot-taxi-business@taxi.yandex.ru

Список установленных на машинке библиотек можно найти тут: [python3.7](https://github.yandex-team.ru/robot-taxi-business/cron_processes/blob/master/python3_libs.txt) и [python2.7](https://github.yandex-team.ru/robot-taxi-business/cron_processes/blob/master/python2_libs.txt)

Список бегущих сейчас скриптов можно посмотреть в файле [_RUNNING.txt](https://github.yandex-team.ru/robot-taxi-business/cron_processes/blob/master/_RUNNING.txt)

**Важно!** Не добавляйте в репозиторий файлы, которые обновляются вашими скриптами. **Это ломает крон!** А лучше вообще избегайте добавления не скриптов в репозиторий

Список токенов, которые доступны роботу можно посмотреть [тут](https://github.yandex-team.ru/taxi/infra-secrets-templates/blob/master/templates/taxi_test_analytics_cron/mylib_config.json.tpl). Некоторые из них используются как дефолтные в библиотеке, но в принципе до всех можно дотянуться кодом:
```python
from business_models.config_holder import ConfigHolder
some_token_name = 'yt_token'
token = ConfigHolder()[some_token_name]
```

Если вам нужно добавить какой-то токен, пишите на taxi-admin@yandex-team.ru что-то в духе: "Добавьте токен с таким-то названием в mylib_config.json пользователя robot-taxi-business на машинку analytics-cron-sas-01.taxi.tst.yandex.net". Передача токена только через [секретницу](http://yav.yandex-team.ru/)! Дайте доступ к секрету абц-сервису "хранение секретов такси в секретнице" на роль "разработчик".

### Как коммитить в business_analytics_cron
Скиньте вот эту ссылку в чат TAXI DWH Help и попросите, чтобы вас добавили в организацию taxi-dwh и команду [analysts](https://github.yandex-team.ru/orgs/taxi-dwh/teams/analysts/members). В организацию могут добавлять только админы организации, пишите в чат DWH Help

Добавлять в команду могут только люди с [ролью Owner в проекте taxi-dwh](https://github.yandex-team.ru/orgs/taxi-dwh/people?query=role%3Aowner) (обычно это тимлиды). Они на [странице команды](https://github.yandex-team.ru/orgs/taxi-dwh/teams/analysts/members) видят зеленую кнопку "Add a member".

### Как установить новый скрипт
0. Создайть/перейти в папку со скриптами вашего подразделения

1. Добавить свой скрипт и запушите изменения в репозиторий
```bash
git add .
git commit -m 'best script ever'
git pull
git push
```

2. Добавить скрипт в crontab_file в репозитории
```bash
  nano crontab_file
```

Робот сам заберет изменения из репозитория из обновит кронфайл

3. Выдать роботу доступы к таблицам, гуглдокам, очередям в трекере и т.п.

4. Логи ваших тасок отправляются на рассылку https://ml.yandex-team.ru/lists/taxi-analyst-cron/ Если хочется их получать, на рассылку нужно подписаться

5. Профит!!!

### Очень медленно работает YQL!
Все запросы запускаются от пользователя [robot-taxi-business](https://staff.yandex-team.ru/robot-taxi-business), у которого нет каких-то дополнительных вычислительных ресурсов. То есть он работает в общем пуле + у него есть ограничение в 8 одновременно бегущих операций. За нагрузкой на робота можно следить [здесь](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=yt_scheduler&tree=physical&dashboard=yt-ui-pool-overview-new&l.pool=robot-taxi-business&b=7d&e=)

В связи со всем этим есть две основные просьбы:
1. Старайтесь писать оптимальные запросы! Это правда важно делать!
2. Если вам скрипт больше не нужен, отключите его, чтобы другие не страдали

Библиотека business_models может помочь обойти в каком-то виде эти ограничения. Для этого:
1. Заведите нового робота на свое подразделение: [инструкция тут](https://wiki.yandex-team.ru/diy/zombik). Подразделение "Сервисы Такси" указывать не рекомендуется - высока вероятность того, что ваша заявка будет отклонена.
Если вашего подразделения нет в списке, его нужно создать [здесь](https://abc.yandex-team.ru/services/taxi/) и подождать, пока оно появится в списке. Роль "Управляющий роботами" в этом случае нужно получить самостоятельно через [IDM](https://idm.yandex-team.ru).
2. Сделайте [robot-taxi-business](https://staff.yandex-team.ru/robot-taxi-business) пользователем своего робота (это нужно, чтобы безопасники не ругались). Это тоже делается через IDM: Стафф -> Управление роботами -> <Имя вашего робота> -> Пользователь, а в качестве сотрудника указать robot-taxi-business.
3. Получите токен к YQL для своего робота (заходим в YQL из-под робота, нажимаем "шестерёнку" в правом верхнем углу - Give me my token!) и добавьте его [в секретницу](https://yav.yandex-team.ru) (как новый секрет, а не как делегирующий токен!).
4. Напишите на taxi-admin@yandex-team.ru просьбу добавить токен вашего робота в mylib_config.json пользователя robot-taxi-business на машинку analytics-cron-sas-01.taxi.tst.yandex.net (передача токена только через секретницу!)
5. Предположим, вы создали робота robot-product и его ключ положили в конфиг под названием robot_product_yt. Есть два способа, как им пользоваться так, чтобы у вас на машинке оно работало так же.

Первый - положить себе в mylib_config.json свой токен под таким же названием. Внутри кода нужно будет добавлять такую конструкцию:
```python
from business_models import hahn
hahn.change_token('robot_product_yt')
```
Дальше вся работа с hahn будет происходить через указанный токен.

Второй способ чуть подлиннее, но не нужно менять свой mylib_config.json:
```python
from business_models.config_holder import ConfigHolder
from business_models import hahn
hahn.token = ConfigHolder().get_any_attribute(['robot_product_yt', 'yt_token'])
```
В этом случае на роботе будет использоваться токен robot_product_yt (потому что он у него есть), а у вас локально yt_token.

6. Если ваш робот читает/пишет/создаёт таблички в YQL, вам нужно запросить соответствующие доступы (лучше всего - через [YT](https://yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//home/taxi-dwh&)) и дождаться, пока их окнут. Но тут есть некоторые нюансы:

- В процессе выполнения запросов практически всегда создаются временные папки, следовательно у робота должен быть доступ к пути //tmp. Для этого необходимо запросить через IDM роль "YT кластер hahn -> Group member", в поле group указываем "yandex" (с маленькой буквы).

Как альтернативный вариант, можно прописать прагму и изменить путь к временной папке:

```pragma yt.TmpFolder = <ваша аналитическая папка>```.

- Чтобы вы могли записывать таблицы (включая временные) в вашу аналитическую папку, вам нужно в том числе запросить в том числе Use-доступ к папке //home/taxi-analytics.

- Если вам нужен доступ к папкам других аналитиков, в IDM нужно написать обоснование вида "в таске TAXIANALYTICS-XXXX я мигрирую свои процессы с робота А на робота Б и мне нужны аналогичные доступы".
