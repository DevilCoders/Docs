## Проблема

Картинки баннеров всегда отдаются в оригинальном размере, что тормозит выдачу.

В сервис feeds, где хранятся баннеры, добавили возможность получения ссылки с шаблонными параметрами размера картинки. Но на данный момент картинки не отдаются, если в шаблон не подставлены размеры. Ввиду критичности данного функционала эту логику не хочется отдавать на фронт, а иметь фоллбек для случая не заданных размеров.

## Предложение

Сделать аналогично картинкам плейсов, которые так же приходят с шаблонами, но при этом отдают оригинал картинки, если не указывать размер.
В данном случае ссылки на картинки задаются в особом формате. На уровне nginx стоит приложение, которое переводит переданную ссылку в формат аватарницы. Написано на Go, дорабатывать не целесообразно.

Предлагается написать ручку, которая будет отдавать картинку. При этом, если не заданы или некорректно заданы размеры изображения будет возвращать оригинал.

В качестве сервиса, в котором это предлагается сделать, рассматривается eats-pics. Изначальная задача этого сервиса - сохранение картинок от пользователей и получение соответствующего url'а. Хочется расширить его возможности для централизованной работы с картинками в Еде через архревью.

Админка сервиса: https://tariff-editor.taxi.yandex-team.ru/services/36/edit/355299/info

Использовать это так: полученную ссылку на картинку из feeds оборачивать в вызов новой ручки.

Например, из feeds пришло:
```
http://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-{w}-{h}
http://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-200-200
```
Оборачиваем в вызов новой ручки:
```
https://eda.yandex.ru/images/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-{w}-{h}
https://eda.yandex.ru/images/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-200-200
```
При вызове произойдет редирект в аватарницу:
```
http://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/orig
http://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-200-200
```

Примерное api ручки:

```
/images/get-{namespace}/{group_id}/{image_name}/{size}:
    get:
        parameters:
          - in: path
            name: namespace
            required: true
            schema:
                type: string
          - in: path
            name: group_id
            required: true
            schema:
                type: string
          - in: path
            name: image_name
            required: true
            schema:
                type: string
          - in: path
            name: size
            required: true
            schema:
                type: string
        responses:
            200:
                description: OK
                headers:
                    X-Accel-Redirect:
                        schema:
                            type: string
```

В данном случае нужно добавить правило на nginx, которое будет делать x-accel-redirect в аватарницу.

Ожидаемая нагрузка, это произведение rps ручки /layout и количества вернувшихся баннеров.

Графики:
- /eats/v1/layout-constructor/v1/layout rps

  https://grafana.yandex-team.ru/d/w1XTf46Wk/nanny_eda_eats-layout-constructor_stable?orgId=1&refresh=30s&viewPanel=68
- Response /eats-communications/v1/layout/banners banners count

  https://grafana.yandex-team.ru/d/jbzlIaHMk/nanny_eda_eats-communications_stable?orgId=1&refresh=30s&viewPanel=39

## Что есть сейчас (подробности)

### Аватарница

Документация: https://wiki.yandex-team.ru/mds/avatars#get

### Картинки плейсов

```
https://eda.yandex/images/3784951/4b6e99209a20e7342d482f7356d0ec5d-{w}-{h}.jpg
https://eda.yandex/images/3784951/4b6e99209a20e7342d482f7356d0ec5d-450x300.jpg
```
проксируются в
```
http://avatars.mds.yandex.net/get-eda/3784951/4b6e99209a20e7342d482f7356d0ec5d/orig
http://avatars.mds.yandex.net/get-eda/3784951/4b6e99209a20e7342d482f7356d0ec5d/450x300
```

Работает с помощью avaproxy - приложение для подбора размера картинок, наиболее близкого к запрашиваемому фронтом.

Код: https://bb.yandex-team.ru/projects/EDA/repos/infrastructure_avaproxy/browse

Формат ссылки:
```
/images/{ava-group}/{img-md5}.{ext}
/images/{ava-group}/{img-md5}-{size}.{ext}
```

### Картинки баннеров

```
https://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/orig
https://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-200-200
https://avatars.mds.yandex.net/get-feeds-media/3683706/65725dc86f11fd2f78821b963954a8cc85a41228/media-{w}-{h} - не работает
```

Доработка в feeds: https://st.yandex-team.ru/TAXIINFRA-3626

Включение шаблонных картинок у баннеров на тестинге:
- https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/FEEDS_SERVICES
  
  "eats-promotions-banner.media.media_name_template": "media-{w}-{h}"
- https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/configs/show/eats_communications_banners_source/
  
  "enable_autoscaling": true - позволяет включать скейлинг изображений на клиенте
