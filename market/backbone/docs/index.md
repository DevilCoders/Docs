# Документация backbone

## Что это?
Принцип организации архитектуры Маркета, при котором выделяют базовый остов из микросервисов, реализующих минимальную функциональность Маркета, и фича-сервисов, расширяющих базовую функциональность.

Данный принцип охватывает только runtime-часть Маркета, т.е. тот функционал, который участвует в обработке запроса пользователю.

## TL;DR
Среди всех сценариев на Маркете выделяем минимальный (сейчас это: карточка -> корзина -> чекаут). Создаем сервисы для обработки этого сценария (backbone-сервисы) и отдаем на поддержку инфраструктуре, остальные сценарии реализуются продуктовыми сервисами. При отказе/деградации одного или нескольких сервисов из продуктового сценария идет переключение на backbone-сценарий (более аскетичный, но стабильный).

## Разработка
- [ABC](https://abc.yandex-team.ru/services/backbone)
