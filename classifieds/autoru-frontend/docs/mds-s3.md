# Использование MDS S3

MDS - яндексовое хранилище файлов. Поверх него есть S3-совместимое API.
Т.о. туда можно заливать различные картинки и файлы в обход пакетов. Структура похожа на файловую.

[Подробнее про MDS и S3](https://wiki.yandex-team.ru/mds/s3-api/)

## Зачем?

Иногда что-то надо выкатывать в обход пакетов, заливать картинки для маркетинга или аппов.
Например, фотографии техников в наших техцентрах, лого сетей СТО, панорамы авто.
В этом случае мы пишем "платформу", а данные хранятся в бункере.
В бункере можно хранить только JSON, а всякие сопутствующие файлы удобно заливать в MDS.
Делать это может даже менеджер, не привлекая разработку и тестирование.

## Адреса

**Прод**:
- endpoint: `http://s3.mds.yandex.net`
- снаружи открыт бакет `vertis-frontend` (сюда надо добавлять файлы руками). Снаружи бакет открыт как `https://yastatic.net/s3/vertis-frontend/`
- снаружи открыт бакет `vertis-front-deploy` (сюда заливаются релизы). Снаружи бакет открыт как `https://yastatic.net/s3/vertis-front-deploy/`

**Тестинг (он нужен только если вы точно понимаете его необходимость)**:
- endpoint: `http://s3.mdst.yandex.net`

Тестинг нужен только для тренировок, дублировать данные в проде и тестинге не надо.
Тестировать там тоже ничего не надо.

## У меня все настроено. Как заливать?

Если не настроено, то читай ниже.

**ВАЖНО**: группируйте файлы по папкам, не надо устраивать свалку. Папку надо именовать максимально понятно, а не максимально коротко.

Некоторые папки:
* `s3://vertis-frontend/autoru-frontend/cert-staff/` - фотки Михаилов
* `s3://vertis-frontend/autoru-frontend/manufacturer-cert-logo/` - логотипы программ сертификации производителей

### Залить одиночный файл
```
$ aws --profile=prod --endpoint-url=http://s3.mds.yandex.net s3 cp <filename.jpg> s3://vertis-frontend/autoru-frontend/<path/to/filename.jpg>

# теперь файл доступен как https://yastatic.net/s3/vertis-frontend/autoru-frontend/<path/to/filename.jpg>
```

### Залить целую папку
```
$ aws --profile=prod --endpoint-url=http://s3.mds.yandex.net s3 cp --recursive <my_local_path> s3://vertis-frontend/autoru-frontend/<my_remote_path>


# теперь файлы доступны как https://yastatic.net/s3/vertis-frontend/autoru-frontend/<my_remote_path>/<файл из папки>
```

## Установка

* На виртуалке (Linux): `sudo apt-get install awscli`.
* На рабочем ноута (MacOS): https://docs.aws.amazon.com/cli/latest/userguide/installing.html

## Настройка

Ключи доступа к s3 в проде можно взять в [Секретнице](https://yav.yandex-team.ru/secret/sec-01e2rbcgtw0dmby415k17cevha/explore/versions).
Ключи для тестинга можно узнать у админов или коллег.

Будет удобно сделать отдельный профиль `prod`.
```
$ cat ~/.aws/credentials
[prod]
aws_secret_access_key = <auto.mds.s3.key.secret из прода>
aws_access_key_id = <auto.mds.s3.key.id из прода>
```

Проверяем
```
# прод
$ aws --profile=prod --endpoint-url=http://s3.mds.yandex.net s3 ls
2017-06-14 16:53:01 adm
2017-06-07 15:59:02 auto
2017-10-31 15:09:24 auto-export
2017-06-14 16:53:07 misc
2017-06-14 16:52:53 realty
2017-06-07 15:56:42 registry
2017-09-07 14:28:33 vertis-feeds
2017-08-25 12:30:33 vertis-share
```

## Использование

[Примеры популярных команд](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#primery)

В большинстве случаев понадобятся только `ls` - посмотреть список файлов и `cp` - залить файл в MDS.

**ВАЖНО**: публично (имеет доступ из браузера снаружи) открыт только бакет `auto-export`!
Для залитых файлов урл будет начинаться с `https://auto-export.s3.yandex.net/`, дальше путь до вашего файла.

Пример:
```
$ aws --profile=prod --endpoint-url=http://s3.mds.yandex.net s3 cp dealer_logo.jpg s3://auto-export/auto/frontend/dealer-logos/dealer_logo.jpg

# теперь файл доступен как https://auto-export.s3.yandex.net/auto/frontend/dealer-logos/dealer_logo.jpg
```
