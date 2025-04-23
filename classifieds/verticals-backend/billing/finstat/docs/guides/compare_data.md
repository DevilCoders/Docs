# Дока "Как сравнить данные в финстате c логом биллинга"

В процессе тестирования финстаты возникло желание сравнить данные в финстате с данными в биллинге для того, чтобы удостовериться, что финстата показывает все корректно. 
Тогда решили, что сравнивать данные в финстате лучше всего с логом [billing_operation_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/billing_operation_event).

Сравнение списаний дилеров делали в [этом тикете](https://st.yandex-team.ru/VSBILLING-5280#620224fc4da8026d5dcfe89e). 
Там написали небольшой [скрипт на скале](https://github.com/YandexClassifieds/verticals-backend/pull/9173) для скачивания данных из финстаты и [yql-запрос](https://yql.yandex-team.ru/Operations/YgIjd1Z1O6hhTFPJ2D_Kie-rzx0aoKJQD9zILy483O4=) для сбора информации из логи биллинга в yt.

Для других потребителей данные в финстате пока не сравнивали.
