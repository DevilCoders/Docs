# Непрочитанные отзывы

Тикет: [https://st.yandex-team.ru/EDAPARTNERS-1817](https://st.yandex-team.ru/EDAPARTNERS-1817), [https://st.yandex-team.ru/EDAPARTNERS-1818](https://st.yandex-team.ru/EDAPARTNERS-1818)

Изменения:
1. Новая ручка `/4.0/restapp-front/eats-place-rating/v1/new-feedbacks/update-view-time` обновляет время последнего просмотра отзывов партнера. Обновляет время у всех ресторанов партнера, если place_ids не передан, иначе только у переданных ресторанов.
2. Новая ручка `/4.0/restapp-front/eats-place-rating/v1/new-feedbacks/check` отдает признак наличия непрочитанных отзывов.

Итоговые спекаи представлены в api.yaml в текущей директории.
