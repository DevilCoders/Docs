# kill 'em all. plus version

цели:
- уменьшить нагрузку на сервис plus
- уменьшить зоопарк покупок в такси - сконцентрировать их в домике

## нагрузка на сервис plus

Текущая инфраструктура сервиса:

```yaml
clownductor_service_info:
    preset:
        production:
            name: x2micro
            overrides:
                cpu: 4
                datacenters_count: 3
        testing:
            name: x2nano
            overrides:
                ram: 8
```

Текущая нагрузка на сервис:

<img src="https://jing.yandex-team.ru/files/erakli00/Screenshot%202021-05-25%20at%2021.45.16.png" width="900">

Как видно, потребляется всего 20% от всех ресурсов, причём оставшиеся проценты потребления нужны только ради следующих вещей:

- продажи подписок через старый нативный флоу
- отображения баннеров на экране поездок
- продажи подписок через старый флоу

Для сравнения, конфигурация сервиса домика Плюса:

```yaml
    preset:
        production:
            name: x2micro
            overrides:
                stable_instances: 2
        testing:
            name: x2nano
            overrides:
                ram: 8
```

Причём домик имеет практически такое же потребление, при этом под него выделено в ~1.5 раза меньше ресурсов:

- 2vCPU x 4 у домика
- 4vCPU x 3 у plus

> **Вывод:** если мы сможем закопать plus, то мы высвободим ресурсы под ~2 продуктовых сервиса, подобных домику Плюса

## вектора продажи плюса в Такси

В хронологическом порядке:

1. вебвью (zoneinfo)
2. нативные банеры (plus)
3. домик (sweet-home)

Старый натив (plus) был раскатан только на Россию, а в зарубежке были вебвью.

Переключение вебвью и баннеров зафиксировано на [вики](https://wiki.yandex-team.ru/users/erakli00/pljus-v-taksi/).

вебвью является фоллбеком для нативных баннеров, но имеет существенный недостаток перед последними: продажа осуществляется через легаси веб-виджет покупки, в котором сильно обрезается воронка продажи подписки. **Нативные баннеры поддерживают нативную покупку одним нажатием.**

## анализ существующей ситуации

### с точки зрения бекэнда

Судя по [статистике](https://yql.yandex-team.ru/Operations/60c9f76c124a7d03d1e456f3) **за неделю в июне** (с 2021-06-08 по 2021-06-15) продажи в **баннерах** происходят только в **ru** (ожидаемо):

|                                              | android | iphone     |
| -------------------------------------------- | ------- | ---------- |
| число продаж                                 | 3416    | 2335       |
| cамая ранняя версия с продажей               | 3.161.0 | 5.35.52976 |
| последняя версия с продажей                  | 4.25.0  | 600.42.0   |
| актуальная версия приложения                 | 4.39.0  | 600.42.1   |

За тот же период **через Домик** наблюдаем [следующую картину](https://yql.yandex-team.ru/Operations/YMoIxQuEI45SmYGnKpWmhRrsmpmXoey6OdeZQ2WesSI=) (ru, Такси):

|                                              | android | iphone     |
| -------------------------------------------- | ------- | ---------- |
| число продаж                                 | 72974   | 63916      |
| минимально возможная версия с Домиком        | 4.18.0  | 600.19.0   |
| самая ранняя версия с продажей               | 4.18.0  | 600.19.0   |
| последняя версия с продажей                  | 4.39.0  | 600.42.0   |
| актуальная версия приложения                 | 4.39.0  | 600.42.1   |

> Под продажей подразумевается поход в ручку `/4.0/plus/v1/subscriptions/purchase` (для баннеров) и `/4.0/sweet-home/v1/subscriptions/purchase` (для Домика).

> Актуальные версии приложений [см. тут](https://st.yandex-team.ru/issues/407430). 
Версии приложений с Домиком можно определить по эксперименту [cashback](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/cashback/current).

На основе этих запросов был составлен файл [backend-purchases.xlsx](./backend-purchases.xlsx).

### с точки зрения метрики

Метрика по России с 2021-06-08 по 2021-06-15 (количество событий):
- вебвью (промо плюса на саммари)
  - [Yandex.Plus.FullScreenPromo.ClickConnectButton](https://yql.yandex-team.ru/Operations/YMtzTb94hoQ5eVhGJLuBFgcM0TCSN0RXXhjYzJSGbBA=) - нажатие на кнопку подключить
  - Yandex.Plus.FullScreenPromo.Shown - показ промо
- баннеры
  - [CashbackBanner.YandexPlusBuySubscriptionTapped](https://yql.yandex-team.ru/Operations/YMtyKBJKfQPR5oOiVgkGO572roZFOW7pU0ryCTr6VJo=) - нажатие на кнопку покупки
- домик
  - [CashbackCard.YandexPlusBuySubscriptionTapped](https://yql.yandex-team.ru/Operations/YMtw7b94hoQ5eVXMToeHsXGlP16_uPJe2dmlTtnZhw8=) - нажатие на кнопку покупки подписки

На основе этих запросов был составлен файл [metrica-purchase-clicks.xlsx](./metrica-purchase-clicks.xlsx).

|                                                | android | iphone   |
| ---------------------------------------------- | ------- | -------- |
| Yandex.Plus.FullScreenPromo.ClickConnectButton | 1072    | 604      |
| Yandex.Plus.FullScreenPromo.Shown              | 11990   | 6890     |
| FullScreenPromo (max version)                  | 3.161.0 | 550.12.1 |
| CashbackBanner.YandexPlusBuySubscriptionTapped | 4159    | 1284     |
| CashbackBanner.Shown                           | 10219   | 8376     |
| CashbackBanner (max version)                   | 4.25.0  | 600.42.0 |
| CashbackCard.YandexPlusBuySubscriptionTapped   | 110651  | 48675    |
| CashbackCard (min version)                     | 3.161.0 | 550.13.0 |

источники:
- https://wiki.yandex-team.ru/taxi/mobile/analytics/#jandeks.pljus
- https://st.yandex-team.ru/ITAXI-3702#5ba22d0029eee2001c03e438
- https://st.yandex-team.ru/TAXIA-12057
- https://st.yandex-team.ru/TAXIANALYTICS-11293

### по платформам

#### android

Соотношение продаж:

- через домик 96%
- через баннеры 4%

Начиная с версии 4.26 в коде есть проверка значений экспериментов, при которой пуш с продажей подписки ведёт на Домик:

```
if buy_plus_native.enabled and cashback.enable_cashback_home_plus_promo:
    open_house()
else:
    open_banners()
```

Отсюда наблюдаем ограничение по последней версии при продажах через баннеры - 4.25.0.

#### ios

Контролы в коде:

- YandexPlusBuyingController - вебвью
- YandexPlusNativeBuyingController - баннеры
- домик

## macro план:

- отключить plus/launch для новых версий
- отключить plus/totw для новых версий
- исследовать необходимость сохранения нативного флоу в домике
- перенос внутренних ручек (пользовательские настройки для МБ)
- переосмыслить таксишные плюшки в сервисе plus
- перенести вебвью из zoneinfo в домик

### отключение старого натива для новых версий приложений

Так как старый натив был только в России, а на территории России сейчас на 100% домик, мы можем заметно снизить нагрузку на plus, отрезав эксперимент `buy_plus_native` по версии.

### нативный флоу

- исследовать, сколько продаж приносит нативный флоу (launch + totw)
- исследовать, какое будет падение продаж при переходе на баннеры
- решить с менеджером необходимость сохранения старого натива в домике

в случае сохранения нативного флоу:
- перенос клиентских ручек (/4.0/plus) в домик
- перенаправление PA в домик

В случае отключения:
- плавно начать отключать клиентский эксп buy_plus_native для старых версий

### перенос внутренних ручек

пока нагрузка на веб-домик у МБ не велика, нужно перенести ручки, в которые они ходят.

- переносим код ручек в домик
  - GET /v1/subscriptions/settings
  - PUT /v1/subscriptions/settings
- направляем МБ в эти ручки

### STQ 

пока оставляем в plus.

## этапы

этапы будут отписаны в тикете https://st.yandex-team.ru/TAXIBACKEND-33966
