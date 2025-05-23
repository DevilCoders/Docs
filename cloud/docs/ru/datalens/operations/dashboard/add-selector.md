# Добавление селектора на дашборд

Перед добавлением селектора убедитесь, что у вас есть право доступа `Редактирование` или `Администрирование` на дашборд. Подробнее см. [раздел](../../security/index.md#permissions).

Чтобы добавить селектор на дашборд:

1. Откройте дашборд.
1. В верхней части страницы нажмите кнопку **Редактировать**.
1. Нажмите кнопку **Добавить** и выберите **Селектор**.
1. Выберите тип селектора:

	{% list tabs %}

	- На основе датасета

		Укажите параметры селектора:

		* В блоке **Общие настройки**:

		  * **Датасет**. Определяет датасет с данными для селектора.
		  * **Поле**. Определяет поле датасета со значениями селектора. Может быть как измерением, так и показателем (подробнее см. [{#T}](../../concepts/dataset/data-model.md#field)).
		  * **Тип селектора**. Определяет тип селектора: выпадающий список, поле ввода или календарь. Тип селектора **Календарь** доступен только для полей датасета типа `Дата` или `Дата и время`. Если в **Поле** выбран показатель, то доступен только тип селектора **Поле ввода**.
		  * **Операция**. Определяет операцию сравнения, по которой селектор фильтрует значения чарта (например, **Равно**, **Больше** или **Меньше**). Если оставить поле пустым, селектор по умолчанию будет фильтровать по операции **Равно**. Список доступных операций зависит от типа поля. Не указывайте операцию, если селектор будет фильтровать QL-чарт.
		  * **Множественный выбор**. Определяет возможность выбора нескольких значений. Опция доступна только для селекторов типа **Список**.
		  * **Диапазон**. Определяет возможность выбора временного промежутка. Опция доступна только для селекторов типа **Календарь**.
		  * **Значение по умолчанию**. Отображается изначально при открытии дашборда.

		* В блоке **Внешний вид**:

		  * **Название**. Определяет название селектора. Используется для выбора селектора при установлении связи с другими виджетами. Опция позволяет управлять отображением названия на дашборде.
		  * **Внутренний заголовок**. Текст, который отображается в селекторе для обозначения операции сравнения. Вы можете изменить значение по умолчанию на свое. Например, для операции **Равно** можно указать значение `=` или `равно`. Параметр доступен только для селекторов типа **Список**.  

		    ![image](../../../_assets/datalens/selector-settings/selector-operation-title.png)

	- Ручной ввод

		Укажите параметры селектора:

		* В блоке **Общие настройки**:

		  * **Имя поля или параметра**. Задает имя поля, по которому можно установить связь селектора с другими виджетами в окне настройки [алиаса](create-alias.md).

		    ![image](../../../_assets/datalens/selector-settings/field-name.png)

		  * **Тип селектора**. Определяет тип селектора: выпадающий список, поле ввода или календарь.
		  * **Операция**. Определяет операцию сравнения, по которой селектор фильтрует значения чарта (например, **Равно**, **Больше** или **Меньше**). Если оставить поле пустым, селектор по умолчанию будет фильтровать по операции **Равно**. Список доступных операций зависит от типа поля. Не указывайте операцию, если селектор будет фильтровать QL-чарт.
		  * **Множественный выбор**. Определяет возможность выбора нескольких значений. Опция доступна только для селекторов типа **Список**.
		  * **Диапазон**. Определяет возможность выбора временного промежутка. Опция доступна только для селекторов типа **Календарь**.
		  * **Значение по умолчанию**. Отображается изначально при открытии дашборда. Это поле необходимо задать обязательно для селектора с типа **Список**, иначе в селекторе не будет доступно ни одного значения.

		* В блоке **Внешний вид**:

		  * **Название**. Определяет название селектора. Используется для выбора селектора при установлении связи с другими виджетами. 

		    ![image](../../../_assets/datalens/selector-settings/caption.png)

		    Опция позволяет управлять отображением названия на дашборде.

		  * **Внутренний заголовок**. Текст, который отображается в селекторе для обозначения операции сравнения. Вы можете изменить значение по умолчанию на свое. Например, для операции **Равно** можно указать значение `=` или `равно`. Параметр доступен только для селекторов типа **Список**. 

		    ![image](../../../_assets/datalens/selector-settings/selector-operation-title.png)
   
   {% if audience == "internal" %}

	- Внешний селектор

		Укажите параметры селектора:

		* В блоке **Общие настройки**:

		  * **Название**. Определяет название селектора. Используется для выбора селектора при установлении связи с другими виджетами.
		  * **Источник данных**. Определяет селектор, созданный в [ChartEditor](../../editor/widgets/selector/external.md).
		  * **Автовысота**. Задает автоматическую высоту для виджета на дашборде.
		  * **Параметры**. Устанавливает список параметров селектора и их значения по умолчанию. Если значения по умолчанию не заданы, на дашборде отобразится ошибка.
   
   {% endif %}
	
   {% endlist %}

   Для [QL-чартов](../../concepts/chart/index.md#sql-charts) в области редактирования чарта на вкладке **Параметры** можно управлять [параметрами селектора](../chart/create-sql-chart.md#selector-parameters), а на вкладке **Запрос** указывать переменную в самом запросе в `not_var{{variable}}` формате.

1. Нажмите кнопку **Добавить**. Виджет отобразится на дашборде.

Ограничения: 

* Для селекторов по показателям доступен только один тип селектора — **Поле ввода**.
* Селекторы по показателям рекомендуется делать только независимыми от других селекторов (необходимо для них задать тип [связи](../../concepts/dashboard.md#link) **Игнор** с другими селекторами в разделе **Связи** при редактировании дашборда).
