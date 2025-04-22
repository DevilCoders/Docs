# Как устроено AБТ в Объявлениях

АБ тестирование — тестирование разных вариантов реализации компонента/логики на непересекающихся группах пользователей.
За разбиение пользователей на группы отвечает сервис [USaaS](https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/uaas/).
Наш фронт делает запрос в proto-ручку USaaS с данными про пользователя, в том числе с yandex-uid.
По умолчанию разбивка делается по yandex-uid, но можно настроить правило в зависимости от других переданных параметров:
https://wiki.yandex-team.ru/users/atayan1/intsrukcija-po-obrashheniju-s-lobzikom/. 
В ответе возвращается список экспериментов и флагов. Дальше этот ответ прокидывается в gateway в GQL extensions, gateway в свою очередь добавляет
эту информацию в мету grpc запросов, которые делает в сервисы.

- Proto-ручка: `http://uaas.search.yandex.net/__protobuf__`
- Документация: https://wiki.yandex-team.ru/users/atayan1/instrukcija-uaas-protobuf-req/res/
- FAQ про админку (в том числе как раскатить на логины со стафа) от Дзена: https://wiki.yandex-team.ru/zen/tech/experiments/instrukcija-po-sozdaniju-jekspov-v-novojj-adminke/#10.kakraskatitjeksptolkonasebja/gruppuljudejj
- Модели: https://github.com/YandexClassifieds/schema-registry/tree/master/proto/general/uaas

## Пример ответа USaaS

```json
{
  "experiments":[
    {
      "testBucket":[
        {
          "testid":"352325",
          "bucket":58
        }
      ],
      "handlers":[
        {
          "components":{
            "CLASSIFIEDS":{
              "stringMap":{
                "test_param":"test_value"
              },
              "intMap":{

              },
              "booleanMap":{

              },
              "floatMap":{

              },
              "stringListMap":{

              }
            }
          },
          "name":"CLASSIFIEDS"
        }
      ]
    }
  ],
  "service":"classifieds"
}
```
В данном примере:

 - testid - выборка в которую попал пользователь
 - test_param - флаг со значением "test_value"

## Как переопределить флаги через url

- Можно передать флаг в урле, для этого нужно указать его тип, проставив соответствующий префикс и отделив его от имени флага двойным подчеркиванием.
  Например, `?exp_flags_stringMap__some_exp_flag=some_value&exp_flags_stringListMap__some_string_list_flag=eniki,beniki,eli,vareniki`.
  Список префиксов [тут](https://github.com/YandexClassifieds/o-frontend/blob/master/general-core/server/lib/req/getUaasHandlerComponentValueFromReq.ts). После перехода по урлу с флагом, его значение запишется в куку и можно будет повторно его не указывать.
- Можно записать флаги в куку `exp_flags`, формат записи - json, структура должна соответствовать типу `THandlerComponentValue` из [модели](https://github.com/YandexClassifieds/o-frontend/blob/master/general-core/models/proto/general/uaas/output.ts)
```json
{
    "stringMap": {
        "flag_name": "flag_value"
    },
    "booleanMap": {
        "flag_name": "flag_value"
    },
    "intMap": {
        "flag_name": "flag_value"
    },
    "floatMap": {
        "flag_name": "flag_value"
    },
    "stringListMap": {
        "flag_name": {
            "stringItem": [ "eniki", "beniki", "eli", "vareniki" ]
        }
    },
}
```
- Можно передать идентификаторы выборок экспериментов, в которые надо попасть, в параметре `?test_ids=<test_id1>,<test_id2>` через запятую или в куке `test_ids` json массивом.

**Важно:**
1. Если указать значения флагов в урле или в куке, то запрос в уаас не будет выполняться.
2. Флаги в урле имеют приоритет над флагами в куке и переписываются в нее.
3. Для очистки оверрайдов флагов и выборок используй параметр `?no_exp_override`

# Как проводить эксперименты

## Ссылки 

 - Документация: https://doc.yandex-team.ru/~search/~experiments/
 - Конфигурация: https://ab.yandex-team.ru/config/186
 - Очередь: https://ab.yandex-team.ru/queue/88
 - Телеграм поддержки: https://t.me/joinchat/CyCSrknStrKg0dT24S2GXA

## Заведение эксперимента

 Форма создания заявки ориентирована на процессы поискового портала. 
 Некоторые настройки, например "Техническое изменение", "Планируется ли выкатывать в продакшен" можно заполнять по
 документации из ссылок либо игнорировать.
 1) Создаем заявку на эксперимент: https://doc.yandex-team.ru/analytics/experiments-guide/concepts/general-info.html
 2) Создаем новый флаг:
    Ссылка: https://ab.yandex-team.ru/flag_storage/flag/__new__
    Видео: https://jing.yandex-team.ru/files/malikov/2018-02-12.mp4
    Handler, Сервис и Компонент: CLASSIFIEDS
 4) Создаем нужные выборки: https://doc.yandex-team.ru/analytics/experiments-guide/concepts/test-ids.html#testid
 5) Задаем значение флагов для каждой выборки: https://wiki.yandex-team.ru/serp/experiments/adminka/testidsformat/
    АБТ предполагает наличие "контрольной" выборки. То есть без каких-либо изменений. То есть без флага.
    Но можно задать для этой выборки какое-то специальное значение флага. 
    И проигнорировать сообщение: "ВНИМАНИЕ: контрольная выборка имеет параметры (не пустая)".
    Пример заполнения флагов: [](ab_flags.jpg)
 6) Шаги Тестирование и Наблюдение пока пропускаем. Cofe метрик у нас пока нет.
 7) Изменяем статус заявки на "В очереди": https://doc.yandex-team.ru/analytics-experiments-instr/rm/1toproduction-autofill/index.html
 8) Открываем на редактирование конфиг:
    В окне конфига https://ab.yandex-team.ru/config/186, нужно перейти к его последней версии с тегом «online» (нажав ссылку с номером версии). 
    Тег «online» имеет конфиг, который сейчас выложен в продакшен. 
    Если вы видите более свежий конфиг с тегом «production», значит кто-то уже создал новую версию конфига.
 9) После этого необходимо завести срез и добавить него выборки: 
    Видео: https://disk.yandex.ru/i/CU5TbMoE7Z9vBA
    Дока: https://doc.yandex-team.ru/analytics-experiments-instr/rm/4configsetting/index.html#kakdobavitizmerenievkonfig
 10) Публикуем эксперимент: проставив тэги «preproduction» и «production»: https://doc.yandex-team.ru/analytics-experiments-instr/rm/1toproduction-autofill/index.html

## Изменение эксперимента

Если нужно добавить новый флаг, поменять выборку и тд в существующем эксперименте нужно: 
 1) Сделать требуемые изменения в выборке.
 2) Сохранить новую версию конфига. Для этого нужно открыть последнюю версию конфига, нажать кнопку "Редактировать"
    и сохранить ничего не меняя. Сами по себе изменения сделанные в выборках никуда не попадут. 

## Метрики

 1) Яндекс.Метрика:
    Можно делать фильтры по test_id в интерфейсе:
    [](ab_metrika.jpg)
    
    Метрика в АБТ: https://ab.yandex-team.ru/metrics/metric
    Документация: 
    https://wiki.yandex-team.ru/jandekspoisk/kachestvopoiska/abt/metrika/#prokinutjeksperimentyvlogimetrikix-yandex-expboxes-crypted
    
 2) Cofe: https://wiki.yandex-team.ru/serp/experiments/cofe/doc //TODO: добавить ссылку когда у нас будут метрики Cofe
