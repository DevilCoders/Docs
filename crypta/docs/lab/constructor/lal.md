Поиск похожих (look-alike)
==

В Лаборатории можно найти пользователей, похожих на тех, которые были найдены по правилу. Дожидаться расчета правила не нужно, можно сразу настраивать look-alike. Время расчета 1-2 дня.

{% note warning %}

В Директе найти похожих пользователей можно прямо [при настройке рекламной кампании](https://yandex.ru/adv/news/look-alike-teper-v-direkte-nakhodite-potentsialnykh-klientov-udobnee-i-bystree). Если вы (или заказчик сегмента) можете воспользоваться этой функцией, не нужно заводить look-alike в Лаборатории.

{% endnote %}

{% note warning %}

Если лал нужен разово, то не нужно делать для него сегмент. В этом случае можно загрузить исходные данные в [Выборки](https://lab.crypta.yandex-team.ru/samples) и в меню `Выгрузка идентификаторов` создать новое представление `Поиск похожих`.

{% endnote %}

## Как настроить look-alike

1. Если look-alike нужен в отдельном сегменте Аудиторий, создаем новый экспорт в Аудитории (копировать в него правило не нужно). Если нужен только look-alike, делаем его в том же экспорте, что и правило.

    Более подробно: 
    Что нужно | Как сделать
    --- | ---
    Нужен только look-alike, исходных пользователей нужно исключить | Делаем look-alike в одном экспорте с правилом, выбираем тип `Только похожие`
    Нужен look-alike вместе с исходными пользователями  | Делаем look-alike в одном экспорте с правилом, выбираем тип `Сегмент и похожие`
    Нужен отдельно исходный сегмент, отдельно look-alike  | Создаем новый экспорт, в нем настраиваем look-alike. **Копировать правило в новый экспорт не нужно**, правило подтянется из соседнего экспорта 

2. Нажимаем на кнопку `LAL`

    ![](https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%202.47.51%20PM.png)

3. Нажимаем на кнопку редактирования

    <img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%202.51.32%20PM.png" alt="drawing" style="width:500px;"/>


4. Проверяем, что подтянулся праивльный id правила. Для этого сравниваем id правила в look-alike с id из правила.

    <img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%202.53.08%20PM.png" alt="drawing" style="width:500px;"/>

    Id правила можно посмотреть здесь:
    <img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%203.15.05%20PM.png" alt="drawing" style="width:500px;"/>

5. Выбираем тип
    
    `Сегмент и похожие` — в look-alike могут попасть пользователи из исходного сегмента.
    
    `Только похожие` — из look-alike будут исключены исходные пользователи.

    <img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%202.21.49%20PM.png" alt="drawing" style="width:500px;"/>

6. Выбираем размер

    Чем выше точность, тем меньше похожих будет найдено.

    <img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%202.22.17%20PM.png" alt="drawing" style="width:500px;"/>

    Если нужно найти заранее определенное количество пользователей, устанавливаем галочку `Точный размер` и указываем его.

    <img src="https://jing.yandex-team.ru/files/terekhinam/exact_size.gif" alt="drawing" style="width:500px;"/>

7. Сохраняем

    <img src="https://jing.yandex-team.ru/files/terekhinam/Screen%20Shot%202021-09-07%20at%202.21.19%20PM-1.png" alt="drawing" style="width:500px;"/>

8. Готово! Look-alike посчитается через 1-2 дня.
