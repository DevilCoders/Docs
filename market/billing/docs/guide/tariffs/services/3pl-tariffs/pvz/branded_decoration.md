# Брендирование ПВЗ

Физический смысл данного тарифа - **единоразовая** выплата БПВЗ за то, что он сделал ремонт по нашему брендбуку.
Тарифы представлены в [оферте, приложение №10, таблица 6.1](https://yandex.ru/legal/pvz/). Размер выплаты зависит от **региона**, в котором открыт пвз.

Выплата происходит раз в месяц (под конец месяца) в "полуручном" режиме:
<ol>
<li> На стороне биллинга логистики смотрим, кому надо начислить за брендовость в текущем месяце
<li> Создаем тикет в очередь MARKETTPLBILL
<li> Призываем ответственного (на дату 1 февраля 2022 года таковым является Виталий Чернецкий) со списком тех пвз, кому мы предположительно должны начислить
<li> Далее ответственный уже говорит точно, кому надо начислить из нашего списка
</ol>

Примеры тикетов: [октябрь](https://st.yandex-team.ru/MARKETTPLBILL-676), [ноябрь](https://st.yandex-team.ru/MARKETTPLBILL-758), [декабрь](https://st.yandex-team.ru/MARKETTPLBILL-838).

В биллинге логистики такая услуга именуется **PVZ_BRANDED_DECORATION**

## В договоре/ДС

Случаев отдельных ДС на данные услугу не было (считаются по общему тарифу)

## В админке Тарифницы

Обратить внимание на:

* pvzTariffZone - тарифная зона, возможны варианты:
  * MOSCOW - Москва
  * MOSCOW_NEAR - Московская область
  * SPB - Санкт-Петербург
  * SPB_NEAR - Ленинградская область
  * OTHER - Остальные регионы

![Мета тарифа для брендирования ПВЗ](../../../../../_assets/images/tariffs/services/3pl-tariffs/pvz/branded_decoration.png)
