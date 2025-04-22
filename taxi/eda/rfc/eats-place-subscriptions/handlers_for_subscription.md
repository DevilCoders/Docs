## Внешние ручки вендорки

Задача:

Сервис `eats-place-subscriptions` должен уметь отдавать информацию о текущей подписке плейса и принимать данные с
вендорки на добавление/имзенение подписки.

**Цель**: реализовать ручки для вендорки для управления подписками.
Требуемые ручки:
- POST `/4.0/restapp-front/v1/place-subscriptions/v1/place/get-subscriptions`: получение информации о текущей подписке плейсов (включая набор фичей в подписке и стоимость) (принимает список плейсов);
- POST `/4.0/restapp-front/v1/place-subscriptions/v1/place/update-subscriptions`: изменение тарифа подписки плейсов (вступает в силу со следующего дня);
- GET `/4.0/restapp-front/v1/place-subscriptions/v1/get-tariffs`: получение всех тарифов, фичей в них и стоимостей, глобально, не по плейсам (без проверки acl).

Макет фичи: [ссылка](https://www.figma.com/file/g8VdGsRnLEUljyNVMwt1vR/Подписка).

Схема АПИ в формате `yaml` приложена в `handlers_for_subscription/api.yaml`. 
