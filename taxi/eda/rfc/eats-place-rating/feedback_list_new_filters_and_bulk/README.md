# Фильтрация отзывов по датам и балковая ручка отзывов

Тикет: [https://st.yandex-team.ru/EDAPARTNERS-1726](https://st.yandex-team.ru/EDAPARTNERS-1726)

Изменения:
1. В ручке `/4.0/restapp-front/eats-place-rating/v1/place-feedbacks` добавлен GET параметр limit - ограничение на выборку записей.
2. В ручке `/4.0/restapp-front/eats-place-rating/v1/place-feedbacks` добавлены GET параметы from и to - границы интервала дат создания отзывов.
3. Ответ ручки `/4.0/restapp-front/eats-place-rating/v1/place-feedbacks` и остальные параметры оставлены без изменений.
4. Добавлена ручка `/4.0/restapp-front/eats-place-rating/v1/place-feedbacks` (POST) для выборки отзывов по нескольким плейсам.

Итоговые спекаи представлены в api.yaml в текущей директории.
