# Настроить платежный аккаунт

Платежный аккаунт {{ yandex-cloud }} потребуется для оплаты счетов за использование {{ tracker-name }} в случае, если [полный доступ](access.md) к сервису получат шесть или более пользователей. Платежи за сервис будут [списываться ежемесячно](pay-the-bill.md#charge) с платежного аккаунта, привязанного к {{ tracker-name }}. Информацию о тарифах и пример расчета ежемесячного платежа вы найдете в разделе [Правила тарификации](pricing.md).

Ответы на распространенные вопросы об оплате услуг вы найдете в разделе [{#T}](payment.md). 

## Привязать платежный аккаунт к {{ tracker-name }} {#bind}

Чтобы использовать платные возможности {{ tracker-name }}, нужно привязать платежный аккаунт. Для этого [перейдите по ссылке]({{ link-bind-ba }}).

Также окно с предложением привязать платежный аккаунт к {{ tracker-name }} появится при выдаче [полного доступа](access.md#set) для нового пользователя (если полный доступ уже есть у пяти пользователей организации) или при включении [автоматического полного доступа](access.md#access-new-users) для всех новых пользователей.

* Если у вас уже есть платежный аккаунт в {{ yandex-cloud }}, выберите его в списке и нажмите кнопку **Привязать**. 

* Если у вас еще нет платежного аккаунта, выберите опцию **Создать** и [добавьте новый аккаунт](#create).

{% note warning %}

Если выбранный платежный аккаунт имеет задолженность или приостановлен, его будет невозможно привязать к {{ tracker-name }}. В этом случае перейдите на страницу [{{ link-billing }}]({{ link-billing }}), выберите ваш аккаунт и следуйте подсказкам в интерфейсе. После того как платежный аккаунт станет активным, снова попытайтесь привязать его к {{ tracker-name }}. Подробнее о статусах аккаунтов читайте в документации [Биллинга {{ yandex-cloud }}](../billing/concepts/billing-account-statuses.md).

{% endnote %}

Если вы привязали платежный аккаунт с действующим пробным периодом или создали новый, для вашего аккаунта будет автоматически активирована платная версия — это значит, что с аккаунта можно будет списывать деньги для оплаты сервисов {{ yandex-cloud }}. Если вы еще не использовали стартовый грант, вы сможете использовать его после перехода на платную версию. Подробнее о стартовом гранте читайте в документе [Начало работы в {{ yandex-cloud }}](../getting-started/index.yaml).

## Создать платежный аккаунт {#create}

1. Откройте [страницу {{ tracker-name }}]({{ link-tracker }}) и [войдите в аккаунт администратора](user/login.md).

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Биллинг**.

1. На странице **Список аккаунтов** нажмите кнопку **Создать аккаунт**.

1. Выберите страну, резидентом которой является плательщик.

1. {% include [choose-name-step](../_includes/billing/choose-name-step.md) %}

1. Если у вас уже есть платежные аккаунты, в блоке **Плательщики** вы можете выбрать одного из доступных плательщиков. Чтобы добавить нового плательщика, выберите **Новый плательщик**.

1. Если вы добавляете нового плательщика:

   1. {% include [choose-type-step](../_includes/billing/choose-type-step.md) %}
   
   1. Укажите ваши личные данные или реквизиты вашей организации.
       
   {% include [contacts-note](../_includes/billing/contacts-note.md) %}

1. Для юридического лица или ИП выберите способ оплаты (банковская карта или банковский перевод).

1. Если вы будете оплачивать услуги от имени физического лица или выбрали оплату банковской картой для юридического лица или ИП, привяжите банковскую карту:

   {% include [pin-card-data](../_includes/billing/pin-card-data.md) %}

   {% include [payment-card-types](../_includes/billing/payment-card-types.md) %}

   {% note info %}
   
   Средства с привязанной карты могут быть списаны только после [активации платной версии](#activate) и использования сервисов {{ yandex-cloud }}.
   
   {% endnote %}

   {% include [payment-card-validation](../_includes/billing/payment-card-validation.md) %}

1. Нажмите кнопку **Создать**.

   {% note info %}

   Нажимая кнопку **Создать**, вы принимаете [оферту {{yandex-cloud}}]({{ link-cloud-oferta }}).

   {% endnote %}

   Платежный аккаунт будет создан в одном из [статусов](../billing/concepts/billing-account-statuses.md):
   
   * `NEW` — для физических лиц-резидентов РФ или РК с любым способом оплаты и юридических лиц-резидентов РФ или РК со способом оплаты **Банковская карта**.
   
   * `PAYMENT_NOT_CONFIRMED` — для ИП и организаций, являющихся резидентами РФ или РК, со способом оплаты **Банковский перевод**, и организаций-нерезидентов РФ и РК с любым способом оплаты. На почту, указанную в аккаунте Яндекса, будет отправлено письмо с описанием дальнейших действий. Активация платежного аккаунта может занять до трех рабочих дней.

   {% if audience == "draft" %}
   
   {% include [account-roles](../_includes/billing/account-roles.md) %}
   
   {% endif %}

После создания платежного аккаунта [привяжите его к {{ tracker-name }}](#bind). Также вы можете использовать стартовый грант для ознакомления с сервисами {{ yandex-cloud }}, если не активировали пробный период и не приобретали платные услуги ранее. Подробнее о стартовом гранте читайте в документе [Начало работы в {{ yandex-cloud }}](../getting-started/index.yaml).

{% if audience == "draft" %}
!!ПОМЕНЯЛИ ЛОГИКУ — теперь при привязке аккаунта он автоматически пытается перейти в платную версию.!!

## Активировать платную версию {#activate}

После создания платежного аккаунта вы можете использовать пробный период и грант для ознакомления с сервисами {{ yandex-cloud }}, если не активировали пробный период и не приобретали платные услуги ранее. Подробнее о пробном периоде читайте в документе [Начало работы в {{ yandex-cloud }}](../getting-started/index.yaml).

В течение 30 дней после окончания пробного периода необходимо активировать в аккаунте платную версию. Также платную версию необходимо активировать, если для вашего аккаунта недоступен пробный период. В противном случае платные возможности {{ tracker-name }} будут недоступны.

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Биллинг**.

1. На странице **Список аккаунтов** выберите платежный аккаунт.

1. На странице **Обзор** нажмите кнопку **Перейти на платную версию**.

1. Включите опцию **Я перехожу на платную версию** и еще раз нажмите кнопку **Перейти на платную версию** для подтверждения.

1. После активации платной версии [пополните баланс аккаунта](pay-the-bill.md). Теперь вы сможете использовать аккаунт для оплаты сервисов {{ yandex-cloud }}.

{% endif %}

## Редактировать платежный аккаунт {#edit}

1. На верхней панели {{ tracker-name }} нажмите ![](../_assets/tracker/tracker-burger.png) → **Биллинг**.

1. На странице **Список аккаунтов** выберите платежный аккаунт, который хотите отредактировать.

   * Чтобы переименовать аккаунт, в блоке с названием аккаунта нажмите значок ![image](../_assets/horizontal-ellipsis.svg) и выберите **Переименовать**.
   
   * Чтобы привязать другую банковскую карту для оплаты, в блоке **Банковская карта** нажмите кнопку **Изменить банковскую карту**.
   
   * Чтобы изменить способ оплаты для юридического лица или ИП, обратитесь в [техническую поддержку]({{ link-tracker-support}}).

   * Чтобы изменить данные плательщика, внизу страницы нажмите кнопку **Редактировать в Яндекс&#160;Балансе**, затем на странице Баланса выберите раздел **Плательщики**.
   
   {% note info %}

   Чтобы изменить название юридического лица или ИНН, [создайте новый платежный аккаунт](#create).

   {% endnote %}
