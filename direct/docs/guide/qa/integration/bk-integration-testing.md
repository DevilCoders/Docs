### Полный цикл интеграции Директ-Модерация-БК-Метрика

{% note warning %}

**Среда для тестирования:** тестируем в проде или на limtest (если по какой-то причине проект не за фичей)   
**Тестовые данные:** [на вики](https://wiki.yandex-team.ru/users/balukov/LoginyDirekt/)  
**Запрос сертификатных денег:** [описано в инструкции](https://wiki.yandex-team.ru/users/ollven/testirovanietransporta/ZachilenieSetrifikatnyxSredstv/)   
**Полезная инструкция про limtest:** [тестирование транспорта](https://wiki.yandex-team.ru/Users/ollven/testirovanietransporta/)

{% endnote %}

1. **Настроить в Директе кампанию**  

- Название и текст объявления должен быть максимально приближенный к реальному, обязательно про Директ.  

 {% cut "Например" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/2022-02-10_12-55-30.png "скрин")

 {% endcut %} 

- Ключевые фразы должны быть реальные, лучше выбирать по ключевым фразам Директа и набором слов, чтобы точно на выдаче увидеть то, что нужно.  
- Создать в Аудиториях [http://audience.yandex.ru/](http://audience.yandex.ru/) геосегмент на БЦ "Бенуа" (или свой домашний адрес) и добавить его в ретаргетинг, чтобы вам не скликали все деньги за 10 секунд, и можно было спокойно протестировать весь цикл вместе со статистикой  
- После создания объявления отправляем кампанию на модерацию и просим staff:sudar или staff:sonick, чтобы они промодерировали вашу кампанию в проде.  
- Ждем пока кампания приедет с модерации, и баннер раскатится в прод - занимает примерно сутки, поэтому важно сделать пункт 3, чтобы к моменту тестирования деньги на кампании еще были.  
  
2. **Увидеть/покликать объявление на выдаче** 
- Открыть вкладку инкогнито, ввести на поиске свой ключевик - должно показаться объявление
- Далее кликаем по нему, если нужно проверить статистику - деньги в этот момент спишутся
- Из консоли берем куку _yandexuid_, с которой увидели баннер, запоминаем ее (можно еще найти в Метрике, если к вашей кампании был привязан счетчик)

3. **Проверяем, что пришло в БК**  
Дергаем ручку БК, в ней содержится информация о том, по каким условиям показалась реклама

`curl -vvv 'http://yabs.yandex.ru/code/2?charset=utf8&additional-banners=6312022016' -H 'X-Yabs-Debug-Output:json' -H 'X-Yabs-Debug-Options-Json: {"logs": true, "mx": false, "keywords": false, "filter_log": true, "match_log": true}' -H 'X-Yabs-Debug-Token:937e098412345678' --cookie 'yandexuid=2829568851466684239 | grep '%21707980%'`

,где:  

`additional-banners`- это id баннера `BannerID` в БК 
`BannerID` можно получить из ручки `https://yabs.yandex.ru/audit/?order-id=21707980`, подставив в нее нужный `order-id` - это id вашей кампании в БК, увидеть его можно в интерфейсе Директа:

 {% cut "Скриншот интерфейса Директа" %}

   ![alt text](https://jing.yandex-team.ru/files/sonick/Kampanii_klienta_Elena_Labkovskaia__sonick-mng10_2018-08-16_22-13-39-aa8fm.png "скрин")

 {% endcut %} 

`X-Yabs-Debug-Token` - это ваш личный токен, он перевыдается каждые 2 часа. Чтобы его получить, нужно дернуть ручку `https://a-shot2.n.yandex-team.ru/update_debug_cookie`
`X-Yabs-Debug-Output` может быть `json` или `proto-text` 

Описание работы этой ручки [по ссылке на вики](https://wiki.yandex-team.ru/bannernajakrutilka/server/quickstartguide/codelabs/#debazhnyjjvyvod)

## Проверка домена в гринурле для смартов 

{% note warning %}

Смотрим всю выдачу по баннеру в цезаре:  
`curl -kv 'https://lookup-profile-caesar.n.yandex-team.ru/lookup_profile/Banners/?BannerID=72057604990701886'`  
[Дока по Цезарю](https://wiki.yandex-team.ru/bannernajakrutilka/server/ytcontentsystem/howtocode/caesar/#kakochenbystrozagljanutvprofil)  

Историю сгенеренных баннеров смотрим [в баннерленде](https://yt.yandex-team.ru/hahn/navigation?path=//home/bannerland/perf/full_state)  
в папке _export_ - текущее значение  
в _archive_ - история  
**DomainID** конкретного показа или клика баннера можно еще посмотреть [в cheventlog'е](https://yt.yandex-team.ru/hahn/navigation?path=//logs/bs-chevent-log)  
в реальный домен можно его превратить через джойн с _//home/yabs/dict/DomainIdToDomain_

{% endnote %}

1. **Смотрим в баннерленд**

[//home/bannerland/perf/full_state/archive](https://yt.yandex-team.ru/arnold/navigation?path=//home/bannerland/perf/full_state/archive)   
**OrderID** - id кампании (бк-шный)  
**GroupExportID** - id группы объявлений  
**BannerID** - у нас таких нет, не пробуем матчить  
**ClientID** - id клиента (можно найти в редактировании клиента)  
**Href** - куда будут вести баннеры  
**Site** - то, что в гринурле будет  
**SiteID** - id домена  

2. **Ищем записи** по своей группе объявлений и домену, с которым показалось или должно показаться объявление. Если все записи с нужным доменом, указанным в фиде, то все ок. Если нет, то заводим баг, так как в **Site** и **SiteID** должен попадать домен из настроек кампании/фида  

Пример запроса:  
`FROM hahn.* WHERE ClientID = 94329915 AND GroupExportID = 4636852926 AND SiteID = 12759379;`
