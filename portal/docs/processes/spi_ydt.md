## Важные договоренности
* Встреча 2021-05-26: при поломках на стыке морда+ПП даунтайм засчитывается в ПП (если проблема на стороне ПП) либо в **горизонталь** морды (если проблема на стороне морды). [Пример инцидента](https://st.yandex-team.ru/SPI-23061)
* Встреча 2021-06-05: YDT-бюджет горизонтали 100 и YDT-бюджет вертикали 250, и YDT вертикали не плюсует в себя YDT горизонтали

## Завести инцидент
[Тикенатор](https://tickenator.z.yandex-team.ru/new-ticket/spi)

{% cut "Как заполнить поля" %}

    * Компонента: portal
    * Сервис: выбирается пострадавшая морда, либо all
    * Контур: prod
    * Датацентр: выбрать ALL или более точно
    * Rollback: поставить галку если пришлось откатывать
    * Заполнить заголовок и нажать Создать

{% endcut %}
## Схема разбора инцидента
[Версия схемы 2021.04.19](https://jing.yandex-team.ru/files/wwax/Screenshot%202021-03-31%20at%2017.53.58.png)
[Последняя версия схемы в draw.io](https://drawio.yandex-team.ru/#Hmorda%2Ftmp%2Fmaster%2Fmorda_spi_flow.xml), коммитится в [github](https://github.yandex-team.ru/morda/tmp)

## Отчеты
[Warden](https://warden.z.yandex-team.ru/components/portal)

## Учебные материалы
Семинар 19.04.2021: [Запись](https://jing.yandex-team.ru/files/wwax/zoom_0.mp4) и [PDF-презентация](https://jing.yandex-team.ru/files/wwax/SPI_VDT_YDT_LSR.pdf)

[Общепортальная вики](https://wiki.yandex-team.ru/9999/)

## Текущий состав клуба девяточников Морды
* [wwax@](https://staff.yandex-team.ru/wwax)
* [dkhlynin@](https://staff.yandex-team.ru/dkhlynin)
* [merzavcev@](https://staff.yandex-team.ru/merzavcev)
* [bdevin@](https://staff.yandex-team.ru/bdevin)




## Термины
**Вертикаль** — совокупность всех сервисов, которые составляют понятие Главная страница для пользователя. [Наша вертикаль](https://warden.z.yandex-team.ru/components/portal).

**Горизонталь** — инфраструктура, бекенд и фронтенд и другие части, которые составляют само ядро Главной страницы без учёта всех смежных сервисов. [Наша горизонталь](https://warden.z.yandex-team.ru/components/portal/s/portal_horizontal).
