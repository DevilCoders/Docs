# Stq send_ride_report_mail

Старый флоу отправки отчета о поездке на почту очень костыльный, можно переписать так, чтобы было удобнее добавлять новые фичи.

## Аргументы stq
* order_id
* locale = None
* personal_email_id = None - мейл, на который нужно отправить отчет
* force_send = False - отправлять отчет, даже если он уже отправлен

(нужно написать скрипт, который ставит эту stq, для тестирования)

## Флоу (примерно совпадает со старым до построения темплейтов)

* Достать информацию по заказу из orders (тут придется ходить прямо в базу). Если заказ не завершен, то то кидаем варнинг и перепланируем sqt через время t (из конфига) (здесь должен быть мониторинг). Если заказ не найден в orders, то ищем в order-proc далее.

* Достаем информацию по заказу из order-proc с помощью archive-api archive/order (ищет в монге, если не найдено - в ыте). Если до этого заказ не был найден в orders, то здесь проверяем завершенность заказа. Проверки на завершенность разные, нужно учитывать структуру orders и order-proc. Если и тут не находим заказ, то кидаем варнинг и  не отправляем отчет (здесь должен быть мониторинг).

* Не нужно отправлять отчет по cargo заказам. Если карго заказ, то пишем это в лог и не отправляем отчет.

* Далее ставим две stq: отправка отчета юзеру и отправка корпового отчета


### Отчет юзеру: stq send_user_ride_report_mail(order_data, locale, force_send)

* Проверяем, нужно ли отправлять отчет юзеру (по базе order_reports_sent) с учетом аргумента force_send.

* Достаем из user-api /users/emails информацию о емейле (personal_email_id и подтвержден ли). Если мейл не подтвержден, смотрим в экспериментальный конфиг SEND_RIDE_REPORT_ALLOW_UNCONFIRMED (по phone_id, зоне, стране), можно ли отправлять на неподтвержденный мейл. Здесь придется оставлять костыль для Латвии и передавать поле is_white_number в эксперимент. Если мейл не найден или не подтвержден и нельзя отправлять на неподтвержденный, то логируем это и не отправляем отчет.


### Отчет корпам: stq send_corp_ride_report_mail(order_data, locale, force_send)

* Проверяем, нужно ли отправлять корповый отчет (по order_proc) с учетом аргумента force_send.

* Достаем локаль и personal_email_id из corp_clients. Здесь тоже можем зафорсить локаль из конфига SEND_CORP_RIDE_REPORT_ALLOW_UNCONFIRMED.

### Далее для юзера и для корпов все одинаково

* Выбираем по конфигу: 
- имя отправителя
- мейл отправителя
- subject
- template_id для main_message
- локаль для main_message
- attachments, для каждого attachment:
	- template_id
	- локаль

выбираем по:
- application
- major_version
- локаль
- бренд
- страна
- зона
- другие необходимые аргументы, например is_white_number для Латвии

* Переводим ключи по локали template и каждого из attachments, подставляем в шаблон. Если не все аргументы из required_args подставились, то кидаем ошибку (здесь должен быть мониторинг).

* Отправляем сообщение (тут надо выпилить часть про смайлик полностью, даже там, где про send_via_sender). Надо несколько раз ретраить, если не получилось отправить, количество и время по конфигу. Если не отправилось, кидаем варнинг и перепланируем (здесь должен быть мониторинг).

* Отмечаем, что сообщение отправлено.

### Структура template

* Базовая информация, которая уже есть к моменту выбора шаблона
```python
@dataclasses.dataclass
class OrderData:
	order: Order
	order_proc: OrderProc
	other_data: OtherData # можно положить еще какую-нибудь нужную информацию
```

* Message - всё сообщение, состоит из данных для отправки сообщения, основого сообщения и аттачментов.
```python
@dataclasses.dataclass
class Message:
	main_message: Template
	attachments: List[Template]
	subject: str
	sender_mail: str
	sender_name: str

	def get_agrs(self, order_data: OrderData) -> Dict[str, Any]:
	    template_args = set()
	    templates = [self.main_message, *self.attachments]
	    for template in templates:
	        template_args.update(template.required_args)
	        template_args.update(template.optional_args)
	    data_fields: Set[_TemplateArg] = set()
	    for template_arg in template_args:
	        data_fields.update(template_arg.value.required_fields)
	        data_fields.update(template_arg.value.optional_fields)
	    # Тут выходит разбивочка по тому из каких баз какие поля нужны
	    # Можно собрать их из базы и сложить в общую кучу
	    data = get_from_db(order_data, [data_field.value for data_field in data_fields])
	    return {template.name: template.get_value(data)}

	def render(self, order_data: OrderData):
		args = self.get_data(order_data)
		rendered_template = self.main_message.render(args)
		rendered_attachments = [attachment.render(args) for attachment in self.attachments]
		return rendered_main_message, rendered_attachments
```

* Шаблон: template_id - уникальное название шаблона, сам шаблон (а также названия его аргументов) будет храниться в базе и доставаться по template_id. Надо написать скрипты на добавление и изменение шаблона в базе. Структуры конкретных шаблонов лучше не реализовывать, чтобы можно было скриптом и экспериментальным конфигом добавить новый шаблон. Аттачменты к письму так же являются шаблонами и рендерятся аналогично.

```python
class Template:
	def __init__(
		self, template_id: str,
		locale: str,
		optional_args_names: List[str]
		required_args_names: List[str]
	):
		self.template_id: str = template_id
		self.locale: str = locale
		self.optional_args: List[_TemplateArg] = [TemplateArg[name].value for name in optional_args_names]
		self.required_args: List[_TemplateArg] =[TemplateArg[name].value for name in required_args_names]

	def render():
		pass
```

* Откуда берутся данные?

Список баз/сервисов, куда можно ходить
```python
class DataProvider(enum.Enum):
    DB_DRIVERS = 'dbdrivers'
    DB_PARKS = 'dbparks'
    ORDER_CORE = 'order-core'

```
Поле из базы
```python
@dataclasses.dataclass(frozen=True)
class _DataField:
    name: str
    provider: DataProvider

```
Все доступные поля
```python
class DataField(enum.Enum):
    driver_middle_name = _DataField('middle_name', DataProvider.DB_DRIVERS)
    driver_last_name = _DataField('last_name', DataProvider.DB_DRIVERS)

```
Аргумент шаблона
```python
@dataclasses.dataclass(frozen=True)
class _TemplateArg(Generic[ValueType]):
    name: str
    description: str
    required_fields: List[DataField]
    optional_fields: List[DataField]
    computer: Callable[[Dict[str, Any]], ValueType]

    @memoize # кешируем
    def get_value(self, data: Dict[str, Any]) -> ValueType:
    	check_required_fields(self.required_fields, data) # проверяем, что в дате есть все обязательные поля
    	data_for_arg = construct_data_for_arg(data) # оставляем только поля, указанные в required_fields или optional_fields
    	return computer(data_for_arg)

```

Все возможные аргументы
```python
class TemplateArg(enum.Enum):
    driver_full_name = _TemplateArg(
        name='driver_name',
        description='Полное имя водителя, собранное из кусочков',
        required_fields=[
            DataField.driver_middle_name,
            DataField.driver_last_name,
        ],
        optional_fields=[],
        computer=_to_driver_name,
    )
    driver_last_name = _TemplateArg(
        name='driver_last_name',
        description='Фамилия водителя, может отсутствовать',
        required_fields=[DataField.driver_last_name],
        optional_fields=[],
        computer=_to_driver_last_name,
    )

```
