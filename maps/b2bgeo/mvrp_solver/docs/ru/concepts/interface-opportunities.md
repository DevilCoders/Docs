# Планирование маршрута через интерфейс


Для запуска планирования необходимо перейти на сайт Яндекс.Маршрутизации и выполнить описанные ниже операции:

1. Перейдите по ссылке [https://yandex.ru/courier/](https://yandex.ru/courier/) и авторизуйтесь, **используя адрес электронной почты указанный при регистрации**.
2. Нажмите меню **Планирование** в левой части экрана
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step2.png" width="620px" />
3. Нажмите **Начать планирование** или выберите файл с настройками автомобилей и заказов:
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step3.png" width="620px" />
4. Выберите качество решения **Быстро** (пробная оптимизация) и нажмите **Начать планирование**.
  Обратите внимание, что планирование с качеством `Быстро` не обеспечивает высокого качества оптимизации. Чтобы получить надежные результаты, используйте режим `Оптимально`.
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step4.png" width="620px" />
5. Загрузите настройки автомобилей и заказов из примера, который вы [скачали ранее](example.md).
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step5.png" width="620px" />
6. Убедитесь, что все настройки автомобилей и заказов загрузились без ошибок - сообщение о наличии ошибок будет в заголовке соответствующего окна.  Демонстрационный пример планирования, с которым вы работаете в данный момент, всегда будет загружен без ошибок.
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step6.png" width="620px" />
7. Оптимизированные маршруты маршруты будут отображены на карте, и в таблице **Маршруты**.
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step8.png" width="620px" />
8. Также вы можете скачать маршруты в формате Microsoft Excel:
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step9.png" width="620px" />

{% note %}
**Поздравляем!**

Вы выполнили первую оптимизацию маршрутов. Теперь вы можете перейти к определению бизнес-требований,
формированию ваших собственных запросов и [оценке экономической эффективности от
внедрения Маршрутизации](economic-effect.md).

Для получения консультации по всем вопросам обращайтесь к вашему менеджеру в Яндекс.Маршрутизации.
{% endnote %}



## Редактирование решения

После выполнения задачи планирования вы можете работать с полученными данными через API, а также можете работать с полученными результатами через интерфейс планирования. В интерфейсе планирования вы можете:

- посмотреть основные метрики результатов планирования;
- посмотреть составленные маршруты на карте;
- посмотреть как заказы распределились по маршрутам;
- отредактировать полученные маршруты и увидеть, как изменятся метрики решения.



Чтобы начать работу с полученным результатом планирования через веб-интерфейс, вам необходимо перейти по ссылке:

`https://yandex.ru/courier/companies/<company_id>/depots/all/mvrp/<task_id>`

где:

- `company_id` – идентификатор вашей компании;
- `task_id` – идентификатор решения, полученный в ответе на запрос выполнения задачи планирования.

Если у вас нет доступа к интерфейсу планирования, или вы не можете найти свой company_id, обратитесь к менеджеру.

В открывавшемся интерфейсе будут видны все спланированные маршруты.

- В таблице "Маршруты" будут отображены метрики по маршрутам и итоговые метрики решения.

- В таблице "Нераспределенные заказы" будут отображены заказы, которые не удалось включить в маршруты с учётом заданных ограничений:
  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_ui.png" width="620px" />

При нажатии на маршрут на карте или в таблице "Маршруты" появится окно "Заказы" с подробной информацией.

Возможности редактирования маршрутов:

- Чтобы исключить заказ из маршрутов доставки, в окне "Заказы" перетащите строку с заказом в таблицу "Нераспределённые заказы". Обратный сценарий тоже поддерживается — заказ из Нераспределенных можно перенести в маршрут или на незанятую машину. Чтобы работать с несколькими элементами, нажмите и удерживайте Ctrl и выделите несколько элементов.

- Чтобы перенести заказ из одного маршрута в другой, перетащите строку с заказом из таблицы "Заказы" таблицу "Маршруты" на строку целевого маршрута, или перетащите точку с заказом на карте на линию другого маршрута.

На текущий момент последовательность посещения точек нельзя отредактировать.

При редактировании маршрутов, система автоматически пересчитывает итоговые показатели построенных маршрутов и при их изменении в таблице «Маршруты» показатели, которые улучшились/ухудшились, будут сопровождаться зелеными или красными значками с указанием разницы изменений по сравнению с первоначальными результатами планирования.

<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_routes.png" width="620px" />

Каждое редактирование обрабатывается системой как отдельная задача, поэтому при каждом внесённом изменении в планирование, генерируется новая ссылка (которая доступна в адресной строке браузера). Если вы хотите сохранить отредактированные результаты, чтобы потом возобновить работу с маршрутами просто сохраните полученную ссылку. Решение и результаты по исходной ссылке при редактировании не меняются.


## Сохранение конечного решения

Если вы закончили редактирование и хотите скачать итоговое решение, нажмите кнопку "Экспортировать" в интерфейсе планирования. Затем, вы можете скачать полученные результаты в формате Excel или JSON.

<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_export_button.png" width="310px" />

Чтобы загрузить результаты планирования в свою систему с помощью ссылки на решение в формате JSON, нажмите "Экспортировать" -> "Экспорт в JSON". В окне экспорта появится ссылка на решение с возможностью её скопировать.

Полученное таким образом итоговое решение нельзя редактировать.

<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_export.png" width="310px" />


<p class="p"><a href="feedback.html" class="xref button">Написать в службу поддержки</a></p>
