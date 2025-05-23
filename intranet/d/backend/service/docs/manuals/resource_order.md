# Создание заявки в кампании на предзаказ

В этом документе описан процесс создания и редактирования заказа на ресурсы.

## Особенности процесса

Заявки на ресурсы распределяются по кампаниям двух типов: _Черновая_ и _Бюджетная_. Процесс создания заявок для разных кампаний одинаковый, но назначение заявок и дальнейшая работа с ними отличаются.

### Черновая кампания

Черновая кампания - это вспомогательная кампания, которую капасити-планеры используют для сбора и анализа потребностей владельцев ABC-сервисов (вас), чтобы на их основе сделать крупноблочные заявки в Бюджетной кампании.
- Заявки из Черновой кампании служат только для уведомления капасити-планнера о долгосрочных потребностях вашего сервиса, они не будут использоваться для дальнейших защит или для автоматической выдачи вашим сервисам заказанных ресурсов.
- Чтобы вы смогли получить нужное вам количество ресурсов, ваш капасити-планер должен учесть ваши пожелания из заявки в Черновой кампании и заложить необходимое количество ресурсов в крупноблочной заявке в Бюджетной кампании.
- Узнать, учел ли капасити-планнер ваши пожелания или нет, вы можете по статусу вашей заявки в Черновой кампании (_Одобрена_ или _Подтверждена_) или явно спросив у капасити-планнера, призвав его в тикет заявки в Черновой кампании.

### Бюджетная кампания

Бюджетная кампания является основной.
- В этой кампании капасити-планнеры каждого направления создают крупноблочные заявки (до 10 штук на направление), объединяющие в себе все потребности сервисов и проектов, за которые они отвечают.
- Заявки из этой кампании защищаются перед Инфра-комитетом и CFO.
- После поставки серверов, ресурсы выдаются по заявкам из Бюджетной кампании в ABC-сервисы, к которым эти заявки привязаны.
- Дальнейшее перераспределение между сервисами направления полученных ресурсов осуществляется капасити-планнером.

### Этапы создания заявки

Процесс создания заявки состоит из:
- заведения заявки и ввода необходимого количества ресурсов;
- подготовки заявки к рассмотрению _Ответственным за capacity-planning_;
- отправки заявки на рассмотрение.

Подготовка заявки к рассмотрению происходит путем заполнения опросника в вкладке Защита при редактировании заявки. Решение о необходимости заполнения опросника принимает _Ответственный за capacity-planning_ вашего VS. Система сбора заявок не блокирует переход заявки на следующий этап (в статус **Готова к защите**) при отсутствии данных в вкладке Защита.

## Заведение заявки

1. Зайдите на <https://abc.yandex-team.ru/> (Каталог сервисов Яндекса)

1. Выберите нужный ABC-сервис

1. Перейдите на вкладку **Заказ железа** выбранного ABC-сервиса

![Вкладка Заказ железа ABC-сервиса](_assets/abc_service_hardware_tab.png "Вкладка Заказ железа ABC-сервиса"){ width="800"}

1. Нажмите на кнопку **Создать заявку** для перехода к форме создания заказа на ресурсы

1. В открывшейся форме заполните информацио о заявке:

	- Укажите название. По названию должно быть понятно, для чего нужны указанные в заявке ресурсы;
	- Выберите ABC-сервис, для которого предназначены заказываемые ресурсы;
	- Выберите _Кампанию_ заказа, к которой будет привязана заявка

	Селект выбора кампаний учитывает наличие у пользователя ролей _Ответственный за заказ ресурсов_ или _Ответственный за capacity-planning_. При отсутствии этих ролей выбор кампании не отображается, заявка создается в _Черновой_ кампании.

	- Отметьте пункт _Критичная заявка_, если без ресурсов из этой заявки ABC-сервис не сможет продолжать работу.

	![Заполнение информации о заявке](_assets/abc_service_hardware_order_information.png "Заполнение информации о заявке"){ width="490"}

1. Выберите провайдеров и ресурсы для заказа, укажите количество

	Количество ресурсов указывается отдельно на каждую дату поставки в виде дельты - **без учета имеющихся ресурсов** ABC-сервиса. Количество провайдеров в одной заявке не ограничено.

	{% note tip %}

	Используйте кнопку Копировать, если вам нужно заказать одинаковое количество ресурсов в нескольких дата-центрах, сегментах или кластерах.

	![Копирование выбранного количества ресурсов](_assets/abc_service_hardware_order_resources_copy.png "Копирование выбранного количества ресурсов"){ width="640"}

	{% endnote %}

	![Выбор провайдеров и ресурсов](_assets/abc_service_hardware_order_resources.png "Выбор провайдеров и ресурсов"){ width="630"}

1. Нажмите кнопку **Сохранить**

## Подготовка заявки к рассмотрению

После сохранения заявки осуществляется переход в вкладку _Защита_. Перейти к заполнению данных также можно при редактировании заявки. Заполнение опросника необязательное.

1. В открывшейся форме опросника выберите причину подачи заявки: _Цель_ или _Естественный рост_. В зависимости от выбора вам будет нужно ответить на разные вопросы.

	![Заполнение вкладки Защита](_assets/abc_service_hardware_order_defense.png "Заполнение вкладки Защита"){ width="630"}

	{% note tip %}

	Качество заполнения опросника прямо влияет на результат рассмотрения заявки. Если по вашим ответам будет трудно понять, для чего нужны указанные ресурсы, заявка будет отклонена.

	{% endnote %}

1. Нажмите кнопку **Сохранить**

	После нажатия на кнопку отобразится карточка созданной заявки на ресурсы. В карточке отображается статус заявки - после создания присваивается статус _Черновик_, и кнопки управления: _Редактировать_, _Отменить_, _Готова к защите_.

	![Карточка заявки](_assets/abc_service_hardware_order_card.png "Карточка заявки"){ width="800"}

## Отправка заявки на рассмотрение

1. Зайдите на <https://abc.yandex-team.ru/> (Каталог сервисов Яндекса)

1. Выберите нужный ABC-сервис

1. Перейдите на вкладку **Заказ железа** выбранного ABC-сервиса

	![Вкладка Заказ железа ABC-сервиса](_assets/abc_service_hardware_tab.png "Вкладка Заказ железа ABC-сервиса"){ width="800"}

1. Найдите в списке нужную заявку на ресурсы

	{% note tip %}

	Используйте фильтр справа для построения нужного списка.

	{% endnote %}

1. Нажмите кнопку **Готова к защите**

	![Кнопки действий с заявкой](_assets/abc_service_hardware_order_card_buttons.png "Кнопки действий с заявкой"){ width="220"}

	После нажатия на кнопку статус заявки изменится на _Готова к защите_. Заявки в этом статусе рассматриваются _Ответственным за capacity-planning_.

## Редактирование заявки

Переход к редактированию доступен из списка заявок или с карточки заявки (доступна по прямой ссылке).

1. Зайдите на <https://abc.yandex-team.ru/> (Каталог сервисов Яндекса)

1. Выберите нужный ABC-сервис

1. Перейдите на вкладку **Заказ железа** выбранного ABC-сервиса

![Вкладка Заказ железа ABC-сервиса](_assets/abc_service_hardware_tab.png "Вкладка Заказ железа ABC-сервиса"){ width="800"}

1. Найдите в списке нужную заявку на ресурсы

	{% note tip %}

	Используйте фильтр справа для построения нужного списка.

	{% endnote %}

1. Нажмите кнопку **Редактировать**

	![Кнопки действий с заявкой](_assets/abc_service_hardware_order_card_buttons.png "Кнопки действий с заявкой"){ width="220"}

	Форма редактирования аналогична форме создания заявки. Для редактирования доступны все поля, кроме ABC-сервиса и кампании заказа.

1. Нажмите кнопку **Сохранить**
