### Назначение 

В этой папке будут собраны джобы, которые мы будем перевозить из ЕДС в номад и другие шедулерные таски.

Актуальную информацию о поселении джоб и работе с ними смотри на вики https://wiki.yandex-team.ru/users/aafa/o-poselenii-periodicheskix-dzhob/


## Сборка проекта

В корневом `Makefile` определены несколько тасок, которые упрощают работу с периодическими джобами

    make job JOB_NAME clean –– очистка assemble директории 
    make job JOB_NAME build –– мавен-билд + докер-билд
    make job JOB_NAME push –– тегирование и пуш докер-имиджа в репу
    make job JOB_NAME run –– спулить докер имидж из репы и запустить его на личной виртуальной машине (адрес хоста берем из файла upload.properties)   
(запускаем из корня проекта)

(!) При этом, `JOB_NAME` — это имя из этого списка https://github.com/YandexClassifieds/auto/blob/5eedbc2d604d8e303dcb77e8b669a4fa9725784c/ext-data-jobs/Makefile#L4-L48. 

Внутри `make` мы формируем полное имя джобы вида `autoru-$(JOB_NAME)-job`

## Деплой в шиву

https://wiki.yandex-team.ru/vertis/search/auto/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA-%D0%BF%D0%B5%D1%80%D0%B8%D0%BE%D0%B4%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D1%85-%D0%B4%D0%B6%D0%BE%D0%B1/#deplojjdzhob

## Старая сборка для номада (DEPRECATED)

Команды можно объединять, например для запуска чистого билда на виртуалке делаем `make job JOB_NAME clean build push run`

    make job JOB_NAME release –– делает чистый билд и пушит имидж с тегом `release_YYYYmmddHHmm` 

release является алиасом для clean build push

### Выкатить в прод (тестинг)
После того, как `make job JOB_NAME release` успешно завершится — появится строка со ссылкой таски на выкладку. 
Выкладываем Дженкинсом.

```
To deploy this image:
1. Go to 
	- [Testing] https://j.vertis.yandex-team.ru/job/Deploys/job/Auto%20ext-data%20batch%20jobs/job/testing/job/autoru-$(1)/build?delay=0sec
	- [Production] https://j.vertis.yandex-team.ru/job/Deploys/job/Auto%20ext-data%20batch%20jobs/job/production/job/autoru-$(1)/build?delay=0sec
2. APP_VERSION = '$(2)'
3. type in any MESSAGE
4. BUILD!

```            

### Как смотреть логи

1. Логи смотреть например вот так: [tail за последний час](https://yql.yandex-team.ru/Operations/Xyu_sBpqvxyEDwVfLjBBOZT4syJ16JG7_km_bxxsQqM=?editor_page=main)

2. Общая [дока по логам](https://wiki.yandex-team.ru/vertis-admin/logs/)

3. Графики [доставки логов](https://grafana.vertis.yandex-team.ru/d/Nu0YzoTWz/vertis-logs?orgId=1&refresh=10s) (если есть какие-то проблемы с доставкой) 
Из списка serviceName выбираем самый последний autoru-sitemap/* 
TODO: позже надо будет добавить агрегацию чтобы упростить работу с этими логами

### Docker repo

registry.yandex.net

Все имиджи будут складываться в этот ^ регистри, с дефолтным тегом или с тегом который будет передан из `env` переменной `DOCKER_REMOTE_IMAGE`

Креды для доступа на пуш смотри [тут](https://wiki.yandex-team.ru/docker-registry/#authorization)

Остальную информацию смотри в [wiki](https://wiki.yandex-team.ru/vertis-admin/registry/) 

    
