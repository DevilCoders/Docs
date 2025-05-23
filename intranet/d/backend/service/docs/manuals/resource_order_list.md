# Просмотр списка заявок на предзаказ ресурсов

В документе описано, как просмотреть общий список заявок и заявки, соответствующие различным критериям.

## Общий список заявок

Для просмотра всех заявок, когда либо созданных в системе сбора заявок, выполните следующие шаги:

1. Зайдите на <https://abc.yandex-team.ru/> (Каталог сервисов Яндекса)

1. Выберите в главном меню **Все заявки**, **Заказ железа**

	![Заказ железа в главном меню](_assets/abc_mainmenu_hardware.png "Заказ железа в главном меню"){ width="700"}

1. Перейдите на страницу **Заказ железа**

	![Страница Заказ железа ABC-сервиса](_assets/abc_service_hardware_page.png "Страница Заказ железа ABC-сервиса"){ width="800"}

Список заявок также доступен на странице каждого ABC-сервиса:

1. Зайдите на <https://abc.yandex-team.ru/> (Каталог сервисов Яндекса)

1. Выберите нужный ABC-сервис

1. Перейдите на вкладку **Заказ железа** выбранного ABC-сервиса

	На этой странице отображаются заявки, созданные для выбранного ABC-сервиса.

	![Вкладка Заказ железа ABC-сервиса](_assets/abc_service_hardware_tab.png "Вкладка Заказ железа ABC-сервиса"){ width="800"}

## Список заявок, соответствующих различным критериям

Список заявок можно фильтровать различным критериям:

- принадлежность к ABC-сервису (выбранный или выбранный с вложенными) - заявки от указанного сервиса и его дочерних ABC-сервисов;
- провайдер - наличие в заявке ресурсов указанных провайдеров;
- название;
- автор;
- ответственный - заявки указанного Ответственного за capacity-planning;
- статус;
- причина - цель или естественный рост;
- тип кампании - черновая или бюджетная;
- дата поставки - заявки, в которых заказаны ресурсы на указанные даты поставки;
- критичная заявка - заявки с отметкой _критичная_, без ресурсов которых сервис не сможет продолжить работу;
- несбалансированные заявки - заявки, в которых ресурсы провайдера YP не сбалансированы между собой по количеству;
- стоимость владения в месяц - диапазон стоимости для общей стоимости владения ресурсами заявки.

![Фильтр по заявкам](_assets/hardware_order_list_filter_1.png "Фильтр по заявкам"){ width="300"} ![Фильтр по заявкам](_assets/hardware_order_list_filter_2.png "Фильтр по заявкам"){ width="300"}


## Статистика

В правой части страницы со списком заявок доступна **статистика** по ресурсам заявок, попавших под фильтр. Данные можно группировать по датам поставки, кампаниям, датацентам или другим характеристикам ресурсов.

![Статистика по заявкам](_assets/hardware_order_list_stat_1.png "Статистика по заявкам"){ width="260"} ![Статистика по заявкам](_assets/hardware_order_list_stat_2.png "Статистика по заявкам"){ width="260"} ![Статистика по заявкам](_assets/hardware_order_list_stat_3.png "Статистика по заявкам"){ width="260"}

## Экспорт

Заявки, соответствующие настройкам фильтра, можно выгрузить в формате .csv по ссылке **Эскпорт**

![Выгрузка xls-отчета](_assets/hardware_order_xls_report.png "Выгрузка xls-отчета"){ width="800"}
