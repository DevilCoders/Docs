# Как проводили нагрузочное тестирование финстаты для autoru

## Общие слова
Цель тестирования состояла в том, чтобы понять выдерживает ли finstat нагрузку.
Finstat - это прослойка между clickhouse и потребителем.
Основное что мы проверяли - насколько эффективные запросы в clickhouse, справляется ли clickhouse с нашим профилем нагрузки.
У finstat grpc-api.

## Какие были альтернативы
Для нагрузочного тестирования сервиса с grpc-api в [чате verticals-tech](https://t.me/joinchat/S__jMZnDO1IEMifF) предложили 2 альтернативы.

[Pandora](https://github.com/yandex/pandora/blob/develop/docs/custom.rst) решение, которое используют в Яндексе.

[И альтернативу на js.](https://k6.io/blog/performance-testing-grpc-services/)
Альтернативу долго не рассматривал, основное решение устроило.

Решил использовать яндексовое решение, т.к по этому пути уже ходили другие команды.
К тому же поддержка в чате яндекс-танка отвечает очень быстро.<br/>
[Инвайт-линк чата поддержки яндекс-танка.](https://t.me/joinchat/BkIYdz-zGT40Ql-TxPZ04A)

## Немного про яндекс-танк

В лунапарке есть разные виды пушек.
- Phantom - описание стрельбы в интерфейсе, но можно стрелять http-запросами, grpc не умеет.
- Pandora - есть встроенная grpc-пушка, описание стрельбы только в конфиге.
Встроенная grpc-пушка подходит для простых кейсов, наш кейс простой.
Помимо встроенной grpc-пушки, можно написать свою пушку на Go.
Встроенная удобна тем, что патроны описываем в json-ами.<br/>
[Дока встроеннной grpc-пушки.](https://wiki.yandex-team.ru/load/pandora/#kakispolzovatvstroennujugrpcpushku)

## Как наливал данные
Для того чтобы тестировать в максимально приближенных к проду условиях, в тестинг перелил данные из прода.<br/>
[Дока как наливать данные.](./upload_history_data.md)<br/>
Коротко - из истории в yt преобразуем данные в нашу модель в clickhouse и заливаем данные в clickhouse
с помощью яндексовой утилиты copy_table_yt_to_clickhouse.
В таблицах в тестинге на данных есть ttl в 30 дней, поэтому если захотим повторить такое тестирование,
данные снова нужно будет наливать.

## Как генерил патроны, с чем столкнулся
[Оценили профиль нагрузки.](https://st.yandex-team.ru/VSBILLING-5303#620b92d7ffa44c30dcbba95b)
Под этот профиль нагрузки сгенерил патроны.
Если меняются данные, то и патроны нужно повторно генерить.

[Из yt достал данные по оплатам.](https://yql.yandex-team.ru/Operations/Yg4SdNJwbE55Smnyg_e9FB-Juyz0siyWKK0--9rEBmA=)
Сохранил их как tskv.
[Превратил их в патроны таким кодом.](https://paste.yandex-team.ru/8417564)
Код не красивый, предполагается что одноразовый.

## Как пострелять
[Ссылка на firestarter.](https://lunapark.yandex-team.ru/firestarter/) <br/>
[Пример конфига.](https://paste.yandex-team.ru/8418163)

#### 1. Как добавить новые патроны.<br/>
Добавляем через интерфейс для phantom, "залить файл".
![button_ammo](../images/button_ammo.png)
Путь до патронов появится в текстовом конфиге phantom.
```
phantom:
    ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/b6d2e173032e4d4d8d43d7afc9d5bdef'
```
Копируем его в src в ресурсы pandora.
````
   resources:
    - dst: ./ammo.json
    src: https://storage-int.mds.yandex.net/get-load-ammo/23470/69900d3ebb6642c1bc17f300834f5d07
````
#### 2. Путь до сервиса прописан в dial_options
```
    gun:
        dial_options:
          authority: finstat-api-grpc.vrts-slb.test.vertis.yandex.net
        target: lb-int-01-sas.test.vertis.yandex.net:80
        type: grpc
```
Мы стреляем через envoy в наш сервис. [Дока наших админов](https://docs.yandex-team.ru/classifieds-infra/deploy/faq/lunapark?)
dial_options и authority команда яндекс-танка доработала для нас ~ за день.

#### 3. Стрелять в балансер можно только с железных танков<br/>
   [список железных танков на 2019 год](https://wiki.yandex-team.ru/load/howto/tankhowto/#tankivrtc) <br/>
   (кажется что он актуальный)<br/>
   [точно актуальный можно получить здесь](https://nanny.yandex-team.ru/v2/services/production_yandex_tank/current_state/instances/) <br/>
    <br/>
   Адрес танка с которого мы стреляем прописан в
```
metaconf:
  enabled: true
  firestarter:
    tank: sas2-7111-25e-all-rcloud-tanks-30169.gencfg-c.yandex.net:30169
  package: yandextank.plugins.MetaConf
```

#### 4. Для информации, дырка в puncher от танков до envoy Вертикалей.<br/>
   [Правило в puncher](https://puncher.yandex-team.ru/?id=5f22e1237c0719994c8c7d73), которое разрешает достреливать до envoy от танков.

#### 5. Нажимаем на кнопку "Огонь", смотрим что произошло.

## В случае если мы дострелили до сервиса
Откроется интерфейс: [ссылка на последнюю успешная стрельба.](https://lunapark.yandex-team.ru/online/2993011#tab=test_data&tags=&plot_groups=main&machines=&metrics=)
В нём в реал-тайме можно будет наблюдать за стрельбой.

## Что делать в случае ошибок
В случае ошибки, переходим в sandbox, там в debug log
ищем по ERROR и внимательно читаем ошибку. Зачастую она понятна.<br/>
[Пример](https://sandbox.yandex-team.ru/task/1267338499/view)

## Что было после стрельбы
Оказалось что наш сервис не держит нагрузку.
Сначала мы поднимали ресурсы для базы. Чтобы это сделать нужно заказать права "Администратор mdb".
[Здесь читать про права в mdb.](https://docs.yandex-team.ru/cloud/managed-clickhouse/security/)
Заказывать в idm.

Затем мы изменили схему в clickhouse(но это другая история).
Затем провели повторную стрельбу и всё было ок.

## Как повторить стрельбу, но что-то поменять в настройках
Зайти на страничку какой-то успешной стрельбы, например
[последняя успешная стрельба](https://lunapark.yandex-team.ru/online/2993011#tab=test_data&tags=&plot_groups=main&machines=&metrics=)
Нажать на неприметный треугольник, раскроются настройки.
![раскрыть настройки](../images/nastrojki.png) </br>
Там взять configinitial.txt и скопировать.
Открыть [firestarter](https://lunapark.yandex-team.ru/firestarter/) и скопировать туда конфиг в виде текста.
Нажать "Огонь".

## Возможно будущее
Возможно админы настроят полигон для стрельб https://st.yandex-team.ru/VOID-1680
На нас проблемы описанные в тикете не влияли, т.к основное что мы проверяли эта работа с базой.
Сам сервис лёгкий и не тормозил.

Возможно нагрузочное тестирование встроят в CI verticals-backend.
Т.к наш код теперь в аркадии, выглядит что это стало проще чем раньше.

## Если понадобится более сложный сценарий

[Дока спамалота как стрелять](https://github.com/YandexClassifieds/etc-mono/blob/master/services/spamalot/gun/README.md). <br/>
В отличие от нас, они для стрельб используют кастомную пушку.<br/>
[Как может выглядеть кастомная пушка на GO.](https://github.com/YandexClassifieds/vs/blob/2e1073874274875ec4089c71f90e13f0fa1fde16/services/vasgen/searcher/load-testing/pandora/Main.go)
