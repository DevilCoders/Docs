# Полезные ссылки

Чат SaaS-support  
https://t.me/joinchat/EweskkTHwZF3144PufRWUg

SaaS FAQ  
https://wiki.yandex-team.ru/jandekspoisk/SaaS/Saas-FAQ/#tekstovyjjpoisk  
Факторы для ранжирования в SaaS  
https://wiki.yandex-team.ru/jandekspoisk/saas/factorsinfo/  
RTYServer. Релевантность. Факторы.  
https://wiki.yandex-team.ru/users/ivanmorozov/relevance/  
О формулах ранжирования в SaaS  
https://wiki.yandex-team.ru/jandekspoisk/saas/formulainfo/#ranzhirovaniesispolzovaniemmatrixnet  
Об устойчивости сортировки  
см. раздел "Q: Документы в моей выдаче переставляются как попало, дублируются на разных страницах, что делать?"  [SaaS FAQ](https://wiki.yandex-team.ru/jandekspoisk/SaaS/Saas-FAQ/#tekstovyjjpoisk).
Компаратор saas url'ов http://bering.search.yandex.net:8080/query-diff/

# Конфигурация SaaS
* SaaS дашборд  https://saas-mon.n.yandex-team.ru/services?my=1  
* конфиги saas - вкладка `config`  
* конфиг релевантностей  - `relev.conf`
* как менять конфиг описано в разделе "Q: Как менять конфиги сервиса?" [SaaS FAQ](https://wiki.yandex-team.ru/jandekspoisk/SaaS/Saas-FAQ/#tekstovyjjpoisk)
* чтобы понять раскатан ли текущий конфиг на бекенды SaaS можно нажать кнопку `diff` на вкладке `Cluster & deploy` дашборда

# Как посмотреть текстовые зоны для документа?
Для определения, в какую зону попал текст, необходимы:
- машина с linux (например, dev виртуалка) с настроенным окружением:
  - [arc](https://wiki.yandex-team.ru/users/igogor/qyppreparation/#nastroilarkadiju)
  - yt (скопировать токен в _.yt_)
- [утилита от saas](https://a.yandex-team.ru/arc/trunk/arcadia/saas/tools/map_to_readable)
  
- [текущий state](https://github.com/YandexClassifieds/vs/blob/master/docs/indexing.md#yt-pull) - важно, чтобы он еще не успел сротироваться на момент запуска скрипта
- путь, по которому хватит прав на создание таблицы

1. Выполняем на dev виртуалке скрипт: 
```shell
arc mount -m arcadia/ -S store/
cd ~/arcadia/saas/tools/map_to_readable
./map_to_readable arnold.yt.yandex.net //home/saas/ferryman-prestable/vasgen_search_lb/ytpull/full.1616524974 //home/verticals/a-sophie/test //home/verticals/a-sophie/test_zones 
```
2. Ждем завершения скрипта
3. Смотрим зоны для конкретного документа в выходной YT таблице ([живой пример](https://yql.yandex-team.ru/Operations/YFo9StK3DOiiOeoVG2zNe5VmUUrdqlRpdoTFdKQCMz0=)):
```sql
SELECT
    `Url`,
    `RootZone`
FROM arnold.`<выходная таблица>`
where Url = 'vasgen/g/<id документа>'
LIMIT 100;
```
4. Отмонтироваться от Аркадии:
```shell
# за пределами Аркадии
cd /home/a-sophie 
arc unmount arcadia
```

# Как катить формулу ранжирования
- подготовить новую формулу, все факторы используемые в полиноме должны существовать в конфиге
- сконвертировать его в бинарный вид с помощью сервиса https://saas-mon.n.yandex-team.ru/polynom_converter?service=vasgen_search_lb
- на странице https://saas-mon.n.yandex-team.ru/service_info?service=vasgen_search_lb&ctype=prestable выбрать конфиг `relev.conf-vasgen_search_lb`
- если для формулы нужна новая модель залить её через кнопку `upload`
- обновить полином в существующей формуле или создать новую формулу
- нажать `submit` (это безопасно, в этот момент конфиги не катятся)
- перейти на страницу https://saas-mon.n.yandex-team.ru/deploy?service=vasgen_search_lb&ctype=prestable и нажать `diff`
- если в диффе есть изменения кроме ваших (особенно другие файлы), спросите дежурных saas и vasgen можно ли это катить
- если катить можно, нужно снять галочку `only safe` и нажать `Deploy`
- будет создана таска по раскатке нового конфига на инстансы бекенда `saas`
- нужно дождаться пока она завершится успешно (все слоты зеленые)
- если таска завершилась неуспешно, нужно поставить галочку `only diff` и снова нажать `Deploy`
- когда выкладка завершена можно убедиться что новая формула работает на тестинге
- затем нужно перейти страницу https://saas-mon.n.yandex-team.ru/deploy?service=vasgen_search_lb&ctype=stable и повторить для `stable` все пункты, начиная с просмотра `diff`
