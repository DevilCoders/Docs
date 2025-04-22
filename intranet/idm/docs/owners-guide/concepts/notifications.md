# Настроить уведомления

Чтобы IDM присылал уведомления о действиях с ролью, выполните следующие действия: 
1. Нажмите на ссылку с вашей системой на странице [**IDM. Все системы**](https://idm.yandex-team.ru/systems).
1. Перейдите на вкладку **Workflow**.
1. Нажмите кнопку **Редактировать**:

   {% cut "Отправлять уведомления для всех подтверждающих" %}
    
   Чтобы IDM присылал уведомление о действиях с [ролью](glossary.md#user-role) всем [подтверждающим](glossary.md#confirmer), а также сотруднику, запросившему эту роль, введите `notify_everyone=True`.
   #### Пример
    
    ```
    approvers = [any_from(['kaushina', 'guitarman', 'gentoonofb', 'yuliya-k'])]
    notify_everyone=**True**
    ```

   {% endcut %}

   {% cut "Отправлять SMS-уведомление" %}

    
    Чтобы IDM отправлял SMS-уведомление о выдаче доступа сотрудникам, у которых на Стаффе указан номер мобильного телефона, введите `send_sms = True`.
	
    {% note alert %}
    
    Если номер телефона на Стаффе не указан, на этапе запроса доступа появится сообщение об ошибке.
    
    {% endnote %}
    
    #### Пример
    
    ```
    approvers = [any_from(['kaushina', 'guitarman', 'gentoonofb', 'yuliya-k'])]
    send_sms=**True**
    ```
    
	{% endcut %}
	
	{% cut "Отправлять уведомления о событиях с ролью" %}    
    
    Чтобы IDM присылал уведомления о событиях с ролью на электронную почту, введите `email_cc=[recipient("email_2", <событие_1>=<True>, <событие_2>=<True> lang='en')]` или `email_cc=["``email_1"``, "``email_2"``]`
    
    Значения:
    - `True` — присылать уведомление.
    - `False` — не присылать уведомление.
    
    Параметры:
    
    - `recipient` — адрес электронный почты получателя (персональная почта сотрудника, общая рассылка).
    - `requested` — роль запрошена.
    - `granted` — роль выдана.
    - `deprived` — роль отозвана.
    - `declined` — роль отклонена.
    - `reminders` — присылать повторные уведомления, если роль ещё не подтверждена. Уведомления отправляются раз в сутки в 9 утра до тех пор, пока роль не будет подтверждена или отклонена.
    - `lang` — язык уведомления. Возможные значения «ru» и «en».
    
    #### Пример
    
    Присылать уведомления на английском языке на общую рассылку doc@yandex-team.ru и сотруднику yuliya-k, если роль была запрошена или отклонена. Во всех остальных случаях уведомления не присылать.
    
    ```
    approvers = [any_from(['kaushina', 'guitarman', 'gentoonofb', 'yuliya-k'])]
    email_cc=['yuliya-k@yandex-team.ru', recipient('doc@yandex-team.ru', requested=True, declined=True, lang='en')]
    ```
    
    Присылать уведомления сотрудникам kaushina и guitarman при любых действиях с ролью.
    
    ```
    approvers = [any_from(['gentoonofb', 'yuliya-k'])]
    email_cc=['kaushina@yandex-team.ru','guitarman@yandex-team.ru']
    ```
    
	{% endcut %}
	
	{% cut "Отправлять уведомления случайно выбранному подтверждающему" %}
	
    Чтобы IDM присылал уведомления случайно выбранным сотрудникам из списка подтверждающих, введите:
    ```
    import random
    approvers = [approver('login_1'), approver('login_2'), approver('login_3')] random.shuffle(approvers)
    approvers = [any_from(approvers)]
    ```
    
    #### Пример
    Подтверждение требуется от любого из указанных, уведомления будут приходить одному из случайно выбранных подтверждающих.
    ```
    import random
    approvers = [approver('ljql'), approver('uruz'), approver('gnoma')] random.shuffle(approvers)
    approvers = [any_from(approvers)]
    ```
    
	{% endcut %}
	
	{% cut "Отключить уведомления для некоторых подтверждающих" %}
	
    Чтобы IDM присылал уведомления о действиях с ролью не всем подтверждающим, а только некоторым из них, в строке `approvers = [any_from..]` введите `notify=True` или `notify=False`.
    #### Пример
    
    Уведомления будут приходить сотрудникам kaushina и guitarman, но не будут приходить yuliya-k и gentoonofb.
    
    ```
    approvers = [any_from('kaushina', 'guitarman', notify=True), any_from('gentoonofb', 'yuliya-k', notify=False)]
    ```
    {% endcut %}
	
	{% cut "Отключить уведомления для всех, кроме запросившего роль" %}
	
    Чтобы IDM присылал уведомление о выдаче роли только сотруднику, запросившему эту роль, введите `no_email = True`
    #### Пример
    
    Присылать уведомление только сотруднику, запросившему роль (подтверждающим не присылать уведомление).
    
    ```
    approvers = [any_from(['kaushina', 'guitarman', 'gentoonofb', 'yuliya-k'])]
    no_email=**True**
    ```
    
    Отключить уведомления для всех, кроме запросившего роль «member» с типом «groups» в группе 8035.
    
    ```
    if role == {'type': 'groups', 'group': "8035", 'role': 'member'}:
    approvers = [any_from(['kaushina', 'guitarman', 'gentoonofb', 'yuliya-k'])]
    no_email = **True**
	```
	
    {% endcut %}    
    
1. Введите комментарий.
1. Нажмите кнопку **Применить изменения**.

