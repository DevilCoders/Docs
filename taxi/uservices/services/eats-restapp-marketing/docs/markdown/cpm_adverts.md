# CPM-реклама

CPM-реклама - это реклама, где деньги списываются с пользователя за показ.
В текущем виде, "показную" механику у нас реализуют только баннеры.

Тикет: [EDACAT-2294](https://st.yandex-team.ru/EDACAT-2294).

## Пайплайн заведения рекламы

![cpm_pipeline](./img/cpm_pipeline.svg)

<!---
@startuml img/cpm_pipeline.svg

:Создаем кампанию и баннеры через ручку
**/4.0/restapp-front/marketing/v1/ad/cpm/create-bulk**;

:Периодика **set-banners-for-moderation** отправляет созданные баннеры в сервис
модерации;

:Модератор в сервисе модераци принимает решение о баннере;

:Результат модерации улетает обратно к нам в ручку
**/internal/marketing/v1/ad/moderation** и ручка ставит stq
**eats_restapp_marketing_add_banner_ads**;

:Обработчик stq подхватывает задачу и создает все нужные сущности в директе
 - кампания
 - группа
 - ключевое слово
 - креатив
 - объявление
 - модерация;

:Срабатывает периодика **update-banner-ids**, которая идет в YT (в дамп CaESaR)
и получает для созданного баннера banner_id из движка БК, после чего сохраняет
этот ID в БД;

:Срабатывает периодика **create-feeds-admin-banner**, которая создает баннер в
feeds-admin;

:Срабатывает периодика **start-cpm-campaign**, которая публикует баннер в
feeds-admin, если он не был опубликован и расписание валидное;

@enduml
-->

## Ручка создания cpm-баннеров

![create_campaigns_handler](./img/create_campaigns_handler.svg)

<!--
@startuml img/create_campaigns_handler.svg

Title Ручка создания рекламы

:Клиент (фронтенд вендорки) посылает запрос в ручку
/4.0/restapp-front/marketing/v1/ad/cpm/create-bulk, чтобы создать новую РК;

:Запрос проходит через eats-restapp-authproxy;

if (пользователь авторизован?) then (нет)
	stop
endif

:Запрос попадает в eats-restapp-marketing;

if (Параметры запроса валидны?) then (нет)
	stop
elseif (Пользователь имеет доступ к управлению ресторанами?) then (нет)
	stop
elseif (Количество ресторанов в запросевалидно?) then (нет)
	stop
endif

:Сохраняем паспортный токен пользователя в БД eats_tokens;

:Загружаем изображение рекламной кампании в feeds-admin;

:Создаем баннеры по количеству ресторанов и сохраняем их в eats_restapp_marketing.banners;

:Сохраняем в eats_restapp_marketing.campaigns рекламную кампанию в статусе not_created;

:Возвращаем пользователю сообщение, что все хорошо и список созданных баннеров;

stop

@enduml
-->

