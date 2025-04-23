# Задача
Избавиться от зависимости от Трекера в качестве гейтвея к источнику стоимостей автомобилей для бека партнёрки.

В существующей реализации бек партнёрского продукта использует стоимость автомобиля как один из признаков для принятия решения о допуске к работе (классификации).
Основной источник данных о стоимости автомобилей для подсистем Я.Такси -- апи авто.ру
Основной потребитель таких данных -- сервис `candidates`.

## Существующий поток данных
В текущем состоянии флоу выглядит приблизительно так:

1. Мануальная проверка стоимости автомобиля саморегом
    1. Трекер принимает запрос на оценку автомобиля с параметрами (марка, модель, год)
    2. Трекер ищет цену авто в монге `dbtaxi.auto_prices` по ключу (марка, модель, год)
        1. Если цена не найдена, она запрашивается из auto.ru по ключу (марка, модель)
           и сохраняется в монге за искомый год
        2. Если цена не найдена в auto.ru за искомый год, она прикидывается
           по (алгоритму приближения)[#Алгоритм приближения стоимости]
        3. Если определение цены невозможно - используется значение по умолчанию "-1"

[![](https://plantuml-wf.test.yandex.net/svg/ZLDBSiCW3Dtd55ecapW7oCARNA7xZeBbX1e3mwTkRb-1FxNZgLjMOFm-4azNetrioHLb-UPGDEIEnmjO9mM1CgQ95lOjkkO4hQb8dU19w0uxuCNN5hg7L0HOVKWVMj81XA6wbaAclVGWDLHKIqqLt4pKbS_Gj0Ov5gvk0R_a6MCmxrdP9my2nODH_xAIrfgb-2cgA2xWWt4ZuOGoDWmIR5QR07LoELqlZIRkiukR7Jeii0FYnKcZJQTx2i-23b2fN8rVWbM0WEvE8LycXzQHpvtL8pNm5ykFI0leNmqUkZ6KiTNMj4XvUdM2Do_OoU-gm-R2NeKZP8PvD51NVDP1waXzab8VkBnFQQBlLVQ-GmjUtZNBrO4SF6HWn9q17Pzoe5wSpjvklb-xkh6d9YllvZ-ddazvo5d8nhnfAPlQO4HhrHDG2DD6XO6ZncCHrsEncrgw4RmrVS1cHA1FGuLHXSdxbAwol8uZNQGXSZtc6m00/)](https://plantuml-wf.test.yandex.net/uml/ZLDBSiCW3Dtd55ecapW7oCARNA7xZeBbX1e3mwTkRb-1FxNZgLjMOFm-4azNetrioHLb-UPGDEIEnmjO9mM1CgQ95lOjkkO4hQb8dU19w0uxuCNN5hg7L0HOVKWVMj81XA6wbaAclVGWDLHKIqqLt4pKbS_Gj0Ov5gvk0R_a6MCmxrdP9my2nODH_xAIrfgb-2cgA2xWWt4ZuOGoDWmIR5QR07LoELqlZIRkiukR7Jeii0FYnKcZJQTx2i-23b2fN8rVWbM0WEvE8LycXzQHpvtL8pNm5ykFI0leNmqUkZ6KiTNMj4XvUdM2Do_OoU-gm-R2NeKZP8PvD51NVDP1waXzab8VkBnFQQBlLVQ-GmjUtZNBrO4SF6HWn9q17Pzoe5wSpjvklb-xkh6d9YllvZ-ddazvo5d8nhnfAPlQO4HhrHDG2DD6XO6ZncCHrsEncrgw4RmrVS1cHA1FGuLHXSdxbAwol8uZNQGXSZtc6m00)

2. Мануальная проверка стоимости автомобиля диспетчером
    1. Cars-catalog принимает запрос на оценку автомобиля с параметрами (марка, модель, год)
    2. Cars-catalog ищет цену авто в таблице `cars_catalog.prices` по ключу (марка, модель, год)
       Сама таблица наполняется при автоматизированной проверке

[![](https://plantuml-wf.test.yandex.net/svg/TOzB2e0m30NtdY9xgGTmuSQ3I8b1YzM4L0LlR_574Sqkdtb3Qfx2CfAQgaAheK4xMyyTv3cK8EgG07l28OEhqgi8ILUaa-90Gefxvc6HX_y6pDjlp1tmOqwx4go8tu1NKdKjXMycEkhhtJC_Ra_73W00)](https://plantuml-wf.test.yandex.net/uml/Kr200EVylEBItDGYNJkxvCIYulZan9B4dFnq1Mrj1Ik5WgBCv5I5v8pKv6mkg7e5P5L0JGNfUiWYUc0jnSZQS_BpiqiBuFgnQz15jrzN5sO03fkHULOAYGK5EPKA-MMfHKMPAQd5sFK0xO1v5s8-K1PY1m00)

3. Автоматизированная проверка стоимости автомобиля в candidates при классификации кандидата
    1. Крона normalize_cars_fields в cars_catalog забирает все автомобили
       из `dbcars.cars` и обновляет таблицы внутреннего PG для выгрузки в кеши candidates.
       Одна из таблиц с кешами, `cars_catalog.prices`, собирается по ценам из монги `dbtaxi.auto_prices`
       и содержит данные по ключу (марка, модель, год) но только для троек (марка, модель, год),
       присутсвующих в монге `dbcars.cars`.
       Недостающие цены прикидываются по такому же (алгоритму приближения)[#Алгоритм приближения стоимости].

[![](https://plantuml-wf.test.yandex.net/svg/bPJTSkCW38Nl-nIwx4wRF41csbVfA20xh35Y-McsRx-2EAvTd4pMLy18dwJZ0nv3CifuT0aKEcqq9efF8D_R6_X-hp343uK9BVTx7uoY286wGF5aN2z1DRPyoyZT-_l8hkUzFfRZIe6N5pZKAB3CG_PpPXEwa_mb3dQx0w2rC3W-kygOauNbeUC0sPa_cU1vn32y2bEJVOKlml0BZ6jhp80PSZuPIu3wjubff288KzU9EcLjOg5ewemZ3KVEJgyHToH8-DViCIV-c0ISb50dGTMZIP6jvfiYjwWReacLc3XSgpGezccgB-CvJgAZpDM4jQCjTmSHHWN2I2l1n4ooTycuJDy_oGVwD9nZdGsUunazHDEx2DWb2d0oAHLVMJxBhihSAa0RFTxhxoZT3RM7ftiOj0irgXArvSWZrNR_goPwRxy0bU8nMxbJkXWhjyPQTsH5n0T-oBt22OSh0sCnB6QRRiwzNFzmx_RbFq3saSAarFnIL0kKsT0ktf4fw69rIIo7woVZ6ldJk_M6hA7VYEO1UQZp2_C6OJjb-qfT47gfm6Dku4yAmUXRERNOBDr6gNy0)](https://plantuml-wf.test.yandex.net/uml/bPJTSkCW38Nl-nIwx4wRF41csbVfA20xh35Y-McsRx-2EAvTd4pMLy18dwJZ0nv3CifuT0aKEcqq9efF8D_R6_X-hp343uK9BVTx7uoY286wGF5aN2z1DRPyoyZT-_l8hkUzFfRZIe6N5pZKAB3CG_PpPXEwa_mb3dQx0w2rC3W-kygOauNbeUC0sPa_cU1vn32y2bEJVOKlml0BZ6jhp80PSZuPIu3wjubff288KzU9EcLjOg5ewemZ3KVEJgyHToH8-DViCIV-c0ISb50dGTMZIP6jvfiYjwWReacLc3XSgpGezccgB-CvJgAZpDM4jQCjTmSHHWN2I2l1n4ooTycuJDy_oGVwD9nZdGsUunazHDEx2DWb2d0oAHLVMJxBhihSAa0RFTxhxoZT3RM7ftiOj0irgXArvSWZrNR_goPwRxy0bU8nMxbJkXWhjyPQTsH5n0T-oBt22OSh0sCnB6QRRiwzNFzmx_RbFq3saSAarFnIL0kKsT0ktf4fw69rIIo7woVZ6ldJk_M6hA7VYEO1UQZp2_C6OJjb-qfT47gfm6Dku4yAmUXRERNOBDr6gNy0)

Из этого следует, что, при переводе саморега на рельсы диспетчерской и окончании жизненного цикла трекера, мы потеряем источник оценки авто.

## Предлагаемый поток данных

1. Мануальная проверка стоимости автомобиля (диспетчером или саморегом)
    1. Каталог принимает запрос на оценку автомобиля (марка, модель, год)
    2. Каталог ищет цену в таблице кешированных ответов от auto.ru `cars_catalog.autoru_cache`
        1. Если запись о цене не найдена или просрочена, она запрашивается из auto.ru по ключу (марка, модель).
           Результат запроса сохраняется в таблицу кешей за все возможные годы с учётом экстраполяции по (алгоритму приближения)[#Алгоритм приближения стоимости]
           Если запись просрочена, но обновление данных по какой-то причине провалилось - продолжаем с просроченными данными.
        2. Если определение цены невозможно - используется значение по умолчанию "-1"

[![](https://plantuml-wf.test.yandex.net/svg/bLD1SeCm33mthz2ndGGUm85B7jBHW99wCBOhoqdp-me32SamJEiBM4Yxw_Loz2wcdhYewmOvVZOeQFrvlwyWi6a8hFTT2l3U8tS7w7rBzW0tGlxOWQxba6A4Sxcib9Z4Sz9jyqLtpBW6Ei9jpHSl6ekYWloXdM0pWWyoLi54e3x83Jm3_GJ3rEQE5Ta3JSdfBmg7DRMl2UgSlxgbdjnl1M9gjFIelJrBMEugbIkCmLiKUiNwf-aL61U91PXYidA78Hj9Qz-9eW0ngqU3JTalRGqQ2zhWV9OhsD5iCP0JDkeWHhYWDG_FoOtlytEuAUUdc9sKlQMO4OPqhOGBLaZ7OQLgwOJp-MQ2BSaOWjLaNFJeHdbtp_TOryVvlyWXuv7e5m00)](https://plantuml-wf.test.yandex.net/uml/bLD1SeCm33mthz2ndGGUm85B7jBHW99wCBOhoqdp-me32SamJEiBM4Yxw_Loz2wcdhYewmOvVZOeQFrvlwyWi6a8hFTT2l3U8tS7w7rBzW0tGlxOWQxba6A4Sxcib9Z4Sz9jyqLtpBW6Ei9jpHSl6ekYWloXdM0pWWyoLi54e3x83Jm3_GJ3rEQE5Ta3JSdfBmg7DRMl2UgSlxgbdjnl1M9gjFIelJrBMEugbIkCmLiKUiNwf-aL61U91PXYidA78Hj9Qz-9eW0ngqU3JTalRGqQ2zhWV9OhsD5iCP0JDkeWHhYWDG_FoOtlytEuAUUdc9sKlQMO4OPqhOGBLaZ7OQLgwOJp-MQ2BSaOWjLaNFJeHdbtp_TOryVvlyWXuv7e5m00)

2. Автоматизированная проверка стоимости автомобиля в candidates при классификации кандидата
    1. Крона normalize_cars_fields в cars_catalog забирает все автомобили
       из `dbcars.cars` и обновляет таблицы внутреннего PG для выгрузки в кеши candidates.
       Один из шагов этого процесса собирает таблицу `cars_catalog.new_prices`
       с ценами по ключу (марка, модель, год) только для троек, присутствующих в `dbcars.cars`
       по алгоритму аналогичному мануальной проверке стоимости (пункт 1.2)

[![](https://plantuml-wf.test.yandex.net/svg/bLHRSiCW3FnEJw7FTjha09vfhz9HZP8m8Q0AwEFs5JWF4xjDmvSDsaMh5MAKP7lBw1Fqw8qrc2ZUWQxdP-3DgaU9hpqcT66pOh4zHH1Q2yMjzHiDgh5bZIENBo_xu3TXPTxATcLvVEng3BWGTfbFk4dWKj4DsR83T0vsFdpwId72AXN3EWXaRzypmVqUPVUab8RS0rW_9Jz1PrA-b8iv1Sdwss-fP7-GF-JVtjNG_iKp9wuUc0DzmnGu3QTW8z2UqpUeMFfYAsIQo1avvTgLv5ioB-i0cqjqS60cpufp2MBkzUXyjbWisgJ6VvqAIO8SdFRSRwmtsjIfwP4aQO_6xDA4ZbmaFTDUYGb8HAjP2behgn0EYlv73gsCX3iwcWBaarYjDKRuG6UdBf5lzox_Y-S-3FMelMqeLkPlGhdYESmaDX1fEeRMU5cJyUNZxx_a8hFJFlpGybapikoAJIp4g3fU1wSxo5oTElJck2cVgjQ7unYolXVQQs7HZORK4JYyZynbivr7nyYBJYuFegKy4qocqssY2lKlH5UGSyzjO9eCXZQim4v29w0V)](https://plantuml-wf.test.yandex.net/uml/bLHRSiCW3FnEJw7FTjha09vfhz9HZP8m8Q0AwEFs5JWF4xjDmvSDsaMh5MAKP7lBw1Fqw8qrc2ZUWQxdP-3DgaU9hpqcT66pOh4zHH1Q2yMjzHiDgh5bZIENBo_xu3TXPTxATcLvVEng3BWGTfbFk4dWKj4DsR83T0vsFdpwId72AXN3EWXaRzypmVqUPVUab8RS0rW_9Jz1PrA-b8iv1Sdwss-fP7-GF-JVtjNG_iKp9wuUc0DzmnGu3QTW8z2UqpUeMFfYAsIQo1avvTgLv5ioB-i0cqjqS60cpufp2MBkzUXyjbWisgJ6VvqAIO8SdFRSRwmtsjIfwP4aQO_6xDA4ZbmaFTDUYGb8HAjP2behgn0EYlv73gsCX3iwcWBaarYjDKRuG6UdBf5lzox_Y-S-3FMelMqeLkPlGhdYESmaDX1fEeRMU5cJyUNZxx_a8hFJFlpGybapikoAJIp4g3fU1wSxo5oTElJck2cVgjQ7unYolXVQQs7HZORK4JYyZynbivr7nyYBJYuFegKy4qocqssY2lKlH5UGSyzjO9eCXZQim4v29w0V)

## Риски
При переключении источника может появиться расхождение в результатах оценки,
которое, попадая в краевые значения классификатора, может изменить ожидаемый результат классификации
Для избежания подобных рисков потребуется провести дополнительное исследование.

## Шаги разработки

1. Добавить таблицу кешированных ответов от auto.ru `cars_catalog.autoru_cache`
1. Добавить таблицу цен для кешей `candidates` - `cars_catalog.prepared_prices`, аналогичную имеющейся `cars_catalog.prices`.
1. Добавить в крону normalize_cars_fields шаг с заполнением таблицы `cars_catalog.prepared_prices` по новому алгоритму.
1. Настроить репликацию заполненной таблицы `cars_catalog.prepared_prices` в YT
   и посчитать среднее отклонение полученной цены и среднюю заполненность (кол-во цен взятых за дефолтную)
   Так можно будет оценить расхождение в получаемых ценах имеющихся в dbcars.cars автомобилей
1. Написать скрипт для того, чтобы прогнать классификацию по данным старого и нового алгоритмов
   (без учёта геозоны) и сравнить результат.
1. Добавить в `cars_catalog` ручку для получения стоимости автомобиля по ключу (марка, модель, год)
1. Заменить походы в существующую ручку трекера на новую ручку cars_catalog
1. Добавить параллельный кеш с новыми ценами в candidates,
1. Выполнять классификацию по новомым ценам параллельно с классификацией по старым ценам,
   записывать результат в логи,
   продолжать принимать решение по старым ценам.
1. Добавить эксперимент для принятия решения какой ценой воспользоваться
   при классификации: новой или старой, по умолчанию - старой.
   Аргументы эксперимента - марка, модель, год, park_id/driver_id, phone_pd_id, license_pd_id.
1. Исправить правила классификации так, чтобы сгладить разницу 
   между класс. по старой и новой цене и переключить эксперимент на новые цены по мере исправления правил.

## Дополнительное предложение
Возможно, во флоу ручной проверки стоимости, перед возвратом стоимости потребителю,
стоит прикапывать стоимость в таблицу `cars_catalog.prepared_prices`.
Это ускорит прорастание стоимости добавляемого авто в candidates, но в кеш станет попадать небольшое кол-во мусорных данных.

## Дополнительная информация

### Алгоритм приближения стоимости
Стоимость автомобиля зависит от года производства, и, чем автомобиль старше, тем он дешевле.
```
total_adjustment_coefficient = (1.0 + yearly_adjustment_coefficient) ** (target_year - closest_known_year)
if abs(total_adjustment_coefficient) > max_allowed_adjustment_coefficient:
    return default_price
return closest_known_year_price * total_adjustment_coefficient
```
Т.е. если мы знаем, что "ВАЗ 2110" 2016 г.в. продаётся на авто.ру за 100_000р., то, принимая коэффициэнт приближения за 0.1, можем предположить, что такая же модель 2014 г.в. должна стоить 80_000р., а 2017 г.в. -- 110_000р.

### Стоимость автомобиля по умолчанию
Если мы не можем найти стоимость автомобиля в авто.ру, или вывести по алгоритму приближения, то, исторически, принимаем стоимость за "-1" и можем продолжить флоу классификации. Это имеет смысл, т.к. некоторые правила классификации не проверяют стоимость авто.
