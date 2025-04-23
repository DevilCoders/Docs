# Возможные точки Б в ППЯ для турбоаппа такси

## Задача
Необходимо сделать (использовать существующую?) ручку, отдающую возможные точки Б для пользователя. Ручка будет использоватся в ППЯ (вызов происходит с бэкенда) для показа пользователю саджестов до захода в турбоапп
https://st.yandex-team.ru/TAXIBACKEND-33949

Со стороны бэкенда главной страницы есть требования к используемым ручкам: 100мс на ответ, нагрузка 2к рпс
Если не получается уложиться, ручка точек Б может быть использована в частях ППЯ с менее жёсткими требованиями ко времени ответа

## persuggest/v1/zerosuggest
Для получения саджестов можно использовать ручку persuggest/v1/zerosuggest  
Ручка предназначена для получения "нулевого" (до того, как пользователь начал вводить адрес в приложении) саджеста  

[Запрос](https://github.yandex-team.ru/taxi/uservices/blob/4b4c435fd04c25f14b434cbdb33f14b8d16129dc/services/persuggest/docs/yaml/definitions.yaml#L1247)  
[Ответ](https://github.yandex-team.ru/taxi/uservices/blob/7f33016d14344ccbf95a4be7072f11694e2ca82a/services/persuggest/docs/yaml/api/4_0_zerosuggest.yaml#L125)  
([Элементы массива в ответе](https://github.yandex-team.ru/taxi/uservices/blob/4b4c435fd04c25f14b434cbdb33f14b8d16129dc/services/persuggest/docs/yaml/definitions.yaml#L1077))

<details>
  <summary>Пример запроса:</summary>
  
```bash
curl --request POST \
    --url http://persuggest.taxi.tst.yandex.net/4.0/persuggest/v1/zerosuggest \
    --header 'content-type: application/json' \
    
    --header 'x-yandex-uid: 4044013613' \

    --header 'x-appmetrica-deviceid: e720ed2e7f3edb450d0e1092fdd25626' \
    --header 'x-appmetrica-uuid: d98e77f3d34d41ca9c6289cf2534f2b1' \

    --header 'x-request-application: app_brand=yataxi' \
    --header 'x-request-language: ru' \
    --header 'x-ya-service-ticket: {ticket}' \

    --data '{
    "type": "b",
    "position": [
        37.43853,
        55.785763
    ],
    "state": {
      "accuracy": 140,
      "app_metrica": {
        "device_id": "38c7693121a99fb921ddcdf35285a2d3",
        "uuid": "c978b63da1eb4fd2932a64fa178f0f89"
      },
      "location": [
        37.53527450561523,
        55.75043869018555
      ]
    }
}'
```
</details>

<details>
  <summary>Пример ответа:</summary>
  
```json
{
  "results": [
    {
      "lang": "",
      "log": "ymapsbm1://geo?ll=37.652%2C55.739&spn=0.001%2C0.001&text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D0%9D%D0%B0%D1%80%D0%BE%D0%B4%D0%BD%D0%B0%D1%8F%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%2C%207",
      "method": "phone_history.destination",
      "position": [
        37.65215398759101,
        55.73951713673424
      ],
      "subtitle": {
        "text": "Москва, Россия",
        "hl": []
      },
      "text": "Россия, Москва, Народная улица, 7",
      "title": {
        "text": "Народная улица, 7",
        "hl": []
      },
      "uri": "ymapsbm1://geo?ll=37.652%2C55.739&spn=0.001%2C0.001&text=%D0%A0%D0%BE%D1%81%D1%81%D0%B8%D1%8F%2C%20%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0%2C%20%D0%9D%D0%B0%D1%80%D0%BE%D0%B4%D0%BD%D0%B0%D1%8F%20%D1%83%D0%BB%D0%B8%D1%86%D0%B0%2C%207",
      "type": "address",
      "image_tag": "custom_suggest_default_tag",
      "city": "Москва",
      "street": "Народная улица",
      "house": "7",
      "tags": [
        "uber_high_relevance"
      ],
      "suggested_tariff": {
        "tariff_class": "uberkids",
        "button_title": "Выбрать тариф $TARIFF$",
        "show_policy": {
          "id": "uberkids_suggest_button",
          "max_show_count": 5,
          "max_widget_usage_count": 1
        }
      }
    },
    ...etc
  ]
}
```
</details>
<br/>

Обсудил с бэком главной, их запрос/ответ устраивает

### Тайминги
На данный момент тайминг persuggest/v1/zerosuggest: [>180мс (98 перцентиль)](https://grafana.yandex-team.ru/d/Hm4D0yGGz/nanny_taxi_persuggest_stable?viewPanel=97&orgId=1&refresh=30s&from=now-3h&to=now)  
Основная зависимость - [umlaas-geo/v1/zerosuggest](https://github.yandex-team.ru/taxi/uservices/blob/dc3bc7f80c08fd2f3346bc5ded45ff6372008400/services/umlaas-geo/docs/yaml/api/zerosuggest_v1.yaml#L15)  
Тайминг umlaas-geo/v1/zerosuggest: [>120мс](https://grafana.yandex-team.ru/d/Hm4D0yGGz/nanny_taxi_persuggest_stable?viewPanel=307&orgId=1&refresh=30s&from=now-3h&to=now)  
  
  
Даже если ходить напрямую в umlaas-geo из бэкенда ППЯ (что сомнительно, т.к. persuggest дополнительно подготавливает ответ), в желаемые 100мс ответ не укладывается.  
Разработчики persuggest планируют ускорять работу ручек сервиса, в том числе zerosuggest, но это ожидается через несколько месяцев  
Одна из составляющих таймингов - rtt, для persuggest он высок, т.к. umlaas-geo распределён по трём ДЦ, наличие ДЦ в man добавляет ~20мс к rtt запроса. Возможно с этим можно что-то сделать (ДЦ-локальные запросы?).  


## Заведение новой ручки
В сервисе persuggest можно завести новую ручку, специально для ППЯ  
По функциональности/логике работы ручка будет аналогична zerosuggest, с учётом того, что некоторые для ППЯ не нужно производить некоторые действия  
Запрос/ответ так же аналогичен zerosuggest
Было бы неплохо иметь возможность контролировать количество адресов, возвращаемых в ответе, но пока можно и без этого

Плюсы:
+ Можно будет развивать в соответсвии с пожеланиями ППЯ, не затрагивая zerosuggest  
+ Т.к. будет меньше логики специфичной для такси, тайминги ручки могут быть ближе к таймингам umlaas-geo/v1/zerosuggest
+ Возможность контролировать ручку, не затрагивая уже существующих потребителей

Минусы:
- Время на разработку




## userplaces (избранные места пользователя)
Т.к. в запросе мы не передаём user_id, userplaces/list отвечает 400, из-за этого в ответ не попадают избранные места пользователя.  
Причина - при запросе в ручку, пытаемся заполнить user_id из auth_context, там это дефолтно инициализированная пустая строка ([клик](https://github.yandex-team.ru/taxi/uservices/blob/7f33016d14344ccbf95a4be7072f11694e2ca82a/services/umlaas-geo/src/views/external/userplaces.cpp#L10)). В ручке стоит регекс валидация ([клик](https://github.yandex-team.ru/taxi/uservices/blob/36155a10aab79b2ec0592dde2896c48210ed416d/services/userplaces/docs/yaml/api/api.yaml#L589)). В результате валидация запроса фейлится.  
Вижу тут следующие решения:
- Получать user_id по yandex_uid
- Не отправлять из umlaas-geo пустой user_id
- В userplaces считать пустой user_id эквивалентным отсутствующему

Первый вариант мне не нравится, т.к. для этого нужен application, и не факт, что по нему найдётся user_id (например, для пользователей, которые никогда не пользовались турбоаппом, но пользовались мобильным приложением)  
Если выбирать между вторым и третьим вариантом, я бы выбрал третий. Хоть он и требует больше разработки, кажется правильнее это обработать в одном месте, чем проверять user_id во всех потребителях


## int-authproxy
После обсуждения решено ходить не напрямую в persuggest, а через int-authproxy.  
Для этого понадобится доработка, т.к. сейчас в этой прокси обязателен user_id, а хедер с yandex_uid (и другие авторизационные хедеры) вырезаются


## Нагрузка
Ожидается 2к рпс, необходимо убедиться, что сервисы участвующие в запросе готовы к этому:
- persuggest
- umlaas-geo
- routehistory
- userplaces
- сервисы карт

## Что делаем
- Доработать int-authproxy и завести в нём правило для проксирования нового запроса
- Завести новую ручку в persuggest, аналогичную по функционалу zerosuggest
- Добавляем сервисам, которые участвуют в запросе zerosuggest ресурсов при необходимости, чтобы они выдерживали новую нагрузку
- Для того, чтобы в ответе были избранные места пользователя - доработать userplaces/list. Доработку можно делать независимо от начала использования zerosuggest
