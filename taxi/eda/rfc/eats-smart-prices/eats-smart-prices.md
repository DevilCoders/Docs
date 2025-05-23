# Сервис рекомендованных цен

## Суть задачи

Хотим предоставить партнёрам возможность включить динамическое изменение цены в заданных пределах.

Система рекомендации будет рассчитывать оптимальную цену каждого айтема с учётом эластичности спроса, популярности и другой статистики по продажам конкретной позиции у данного ресторана и/или в сети ресторанов и/или похожего блюда в других ресторанах и/или похожей категории блюд в других ресторанах (далее - Статистики), так чтобы либо общее число заказов не изменилось значительно, либо чтобы результирующий оборот был больше исходного (в зависимости от партнёра).

Данная опция будет платной для партнёра, размер платы — процент от динамической части цены проданного айтема.

## Какие компоненты затрагивает задача

1. Ресторанное приложение: партнёр указывает диапазон динамического изменения цены.
1. Клиентское приложение: везде должны показываться финальные цены, а не стартовые.
1. Процессинг заказа: нужно понимать какая часть стоимости заказа является базовой, а какая динамической, для дальнейшего вычисления стоимости услуги.
1. Биллинг: нужно начислять обычную комиссию на базовую стоимость заказа, и стоимость услуги для динамической части. Также нужно доработать отчёты, чтобы партнёр мог проследить за что были удержаны какие суммы.
1. Интеграции: для партнёров на интеграциях нужно реализовать создание заказов по исходной цене (там где партнёры валидируют цены), а также доработать кастомные отчёты.

## Особенности реализации

- Динамическое ценообразование несовместимо со скидками на меню: если партнёр заводит скидку, она применяется к базовой цене.
- При начислении баллов плюса баллы начисляются на финальную стоимость блюд по обычной логике.
- При вычислении штрафа за отмену заказа, штраф назначается в размере базовой комиссии, применённой к финальной стоимости блюд (включая динамическую часть), при этом дополнительно опция динамической цены не оплачивается.
- Любые изменения формулы, максимального значения динамической части, влияния динамической части на стоимость конкретных блюд начинают действовать начиная с 00 часов следующего дня по местному времени ресторана (за исключением полного отключения фичи, оно будет применено сразу).

## Техническая реализация

### Сервис рекомендации цен

Будет создан сервис, отвечающий за логику динамического изменения цены блюд, а также база данных к нему.

Сервис будет отвечать за:

1. Хранение и изменение максимального диапазона изменения цены блюд в ресторане: изменяется из рестапа или через админку (в первоначальной версии запуском скриптов).
1. Вычисление рекомендованной цены айтема на основе базовой цены, идентификатора и названия айтема, категории, плейса, бренда и Статистики.
1. Обеспечение стабильности цен (при условии неизменности базовой цены айтема) в пределах суток по местному времени ресторана.

Пишем на uservices, [код](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-smart-prices), [спека](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-smart-prices/docs/yaml/api)

Делаем две ручки для ресторанного приложения: получить инфу по списку ресторанов, обновить инфу по списку ресторанов

В ручке получения проверяем авторизацию (через auth-proxy) и проверяем, что у пользователя есть доступ ко всем ресторанам из запроса.
Дальше простой селект из базы и формирование ответа.

В ручке обновления помимо проверок доступов нужно во-первых определить время, начиная с которого нужно применить изменение, а во-вторых посчитать возможные варианты изменений цен.

Для определения времени либо берём дату из запроса, либо берём текущую дату в таймзоне ресторана и прибавляем 1 день.
Время определяем исходя из расписания ресторана: если ресторан закрывается на ночь, то берём середину интервала между закрытием и открытием, иначе 3 часа ночи в таймзоне ресторана (чтобы уменьшить кол-во пользователей которые увидят изменение).

В базу по плейсам сохраняем id ресторана, новое значение, время начала использования, id пользователя который внёс изменение, имя эксперимента, который будет применён для пользователей при запросе данных этого ресторана (см. далее), updated_at. Если есть предыдущее сохранённое значение, выставляем ему таймстемп завершения и updated_at.

Запускаем расчёт вариантов наценок: аналитики будут периодически создавать сегменты ресторанов и для каждого сегмента выбирать название эксперимента, который за него отвечает и максимальную наценку, которую мы считаем приемлемой.

На старте используем для всех айтемов одинаковую наценку, делаем три группы: без наценки (контроль), 50% от максимума, 100% от максимума. Действительный размер наценки определяется в рантайме по эксперименту в библиотеке.

Чтобы была возможность в будущем делать разную наценку на разные блюда, нам нужно хранить в отдельной таблице данные для каждого айтема ресторана.
Но так как меню может меняться, чтобы не отслеживать постоянно эти изменения, предусмотрим возможность указать дефолт на ресторан и категорию.

Делаем следующие столбцы в таблице: place_id, category_id(opt), item_id(opt), values(json или integer array), start, end(opt), updated_at

Соответственно если не указаны category_id и item_id это дефолт на ресторан, если не указан только item_id, то это дефолт на категорию.

### Рестап

Для реализации фичи в вебе рестапа будет сделана форма управления услугой.
Для отображения данных будет использован метод получения статуса фичи по набору плейсов `POST /4.0/restapp-front/smart-prices/v1/status`
Для модификации будет использован метод апдейта диапазона изменения фичи (в процентах) по набору плейсов `POST /4.0/restapp-front/smart-prices/v1/update`.
[Спека](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-smart-prices/docs/yaml/api/partner_settings.yaml).

Тикет на разработку: [EDARESTAPP-4305](https://st.yandex-team.ru/EDARESTAPP-4305)

### Кэширующая библиотека

Так как в данном проекте критически важно чтобы клиенту никогда не показывались базовые цены, помимо сервиса будет реализована кеширующая библиотека.
Библиотеку нужно будет подключить в сервисах

1. eats-restaurant-menu
1. eats-cart
1. eats-upsell
1. eats-full-text-search

Вообще, логику преобразования цены нужно реализовывать в сервисе хранения меню, но он сейчас находится на стадии тестирования и не будет готов к моменту запуска нашей фичи.

В сервисах меню, апсела и поиска нужно просто подменять базовую цену на рекомендованную при отдаче ответа.
При этом нужно учесть, что наценка не применяется к айтемам со скидкой.

Для этого нам нужно сделать кэш данных сервиса.

Кэш будет инкрементальный по updated_at.

В первом запросе на холодную, будем отдавать из сервиса только текущие активные данные и данные в будущем, а также updated_at последнего изменения. Дальше запрашиваем по условию время обновления >= updated_at.

Что храним: для каждого ресторана имя эксперимента, который сейчас используется -- возможно в процессе реализации упростим.

Для айтемов (с учётом дефолтов) массив модификаторов и временное окно, в котором оно действует (обычно без правой границы).
При этом нет смысла хранить данные в прошлом, поэтому когда при запросе мы находим данные, у которых дата завершения прошла, удаляем их.

При обработке запроса: получаем из кэша имя эксперимента и модификаторы для всех айтемов в запросе, ходим в эксп с device_id пользователя, получаем индекс модификаторов, который нужно применить, подменяем цены, запускаем функцию округления (TODO, вероятно в отдельной задаче: продумать продуктово, как округляем: до 99 рублей, до 50, до 10, до рубля, до .99 копеек, исходя из базовых цен плейса).

### Доработки в коре (как запасной вариант)

Есть почти единое место, откуда сейчас на проде пользователи получают меню. Это кора и табличка `place_menu_items` в её базе.

Положить прямо в базу кэш со списком модификаторов, start, end со связью 1 к 1 на айтемы. Тогда мы сможем передавать все модификаторы сразу с исходными ценами, в библиотеке останется только логика выбора конкретного модификатора и округления.

В коре нужно будет завести крон-таску, которая по аналогии с написанным выше будет наполнять кэш в базе.

Недостатки: нужна разработка на php в deprecated сервисе, не подходит для поиска, так как там цены берутся не напрямую из коры, а из кеша в эластике. Но для поиска можно либо скрыть цены (если не будем успевать к запуске), либо сделать кэш по описанному выше подходу.

### Доработки в корзине

В сервисе корзины нужно сохранять и базовую и финальную стоимость айтемов, в клиентских ручках и во всей логике работы использовать только финальную стоимость.

В ответе запросов `/internal/eats-cart/v1/lock_cart` и `/internal/eats-cart/v1/lock_cart_pickup` добавляем в информацию об айтеме размер динамической части стоимости айтема.

В объект ответа в каждый объект из массива `items` добавляем опциональное поле `dynamic_part_amount` с суммой динамической части стоимости одной единицы данного айтема.

### Доработки в процессинге, ревизии заказа

В `order_revision_items` добавляем опциональное поле `dynamic_part_amount` (скорее всего через отдельную табличку со связью 1 к 1), которое заполняем данными из ответа корзины.

В `order_revisions` при расчёте поля `cost_for_place` используем финальную цену айтема (по сути, ничего не меняем, потому что корзина в стоимости айтемов как раз присылает финальную сумму)

Меняем провайдер для биллинга в коре: нужно посчитать отдельно стоимость базовой части заказа и динамической.

Тикет на разработку: [EDAORDERS-7543](https://st.yandex-team.ru/EDAORDERS-7543)

Не забыть проверить изменение заказа из вендорки: там в заказ отправляются базовые цены, и именно они будут зафиксированы в заказе.

### Доработка в админке еды

Доработки не требуются, потому что в `cost_for_place` будет финальная стоимость заказа для ресторана.

### Доработка в интеграциях

Необходимая часть – при отправке запроса в api партнёру, в ценах айтемов передавать именно базовую цену, для партнёров, которые возвращают ошибку при несовпадении цены.

Для этого нужно смотреть на поле `dynamic_part_amount` айтема и если оно не null, то отправлять вычитать его значение из цены айтема, иначе использовать старую логику.

Тикет на разработку: [EDADEVINT-1](https://st.yandex-team.ru/EDADEVINT-1)

### Доработка в биллинге

Нужно продолжать брать базовую комиссию с `cost_for_place` - сумма всех `dynamic_part_amount * quantity` и добавить удержание стоимости опции с суммы `dynamic_part_amount * quantity` (расчёт сумм будет в провайдере по задаче [EDAORDERS-7543](https://st.yandex-team.ru/EDAORDERS-7543)). Размер удержания желательно брать из конфига/эксперимента с возможностью задать разный процент для разных плейсов/партнёров.

Для этого добавляем логику в обработку событий order_create и order_change.

Также добавляем в tlog новый тип – стоимость услуги динамического ценообразования. И пишем удержанную сумму с этим типом.

Нужно добавить дополнительную информацию о суммарном размере разницы финальных и исходных цен айтемов (`dynamic_part_amount`), а также сумму удержанной из неё стоимости опции в ежемесячные отчёты.

Для ежемесячных отчётов пока драфт такой (все названия рабочие, не для прода):

- поле "сумма по заказу" становится суммой по заказу без наценки
- добавляем поле "сумма по заказу с учётом динамической цены"
- добавляем поле "сумма инкремента"
- добавляем поле "стоимость опции 'рекомендация цены'", абсолютное значение
- добавляем поле "общая стоимость услуг Яндекса" с суммой комиссии и стоимости опции.

Тикет: [EDABILLING-560](https://st.yandex-team.ru/EDABILLING-560)
