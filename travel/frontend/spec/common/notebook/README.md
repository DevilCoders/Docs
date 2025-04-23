# Notebook

Методы для записной книжки пассажира

Данные описаны в camelCase (кроме getDocumentTypes), хотя записная книжка работает только со snake_case. Преобразование к camelCase происходит на фронтовой ноде (так сделано, чтобы потом проще было перейти на camelCase на бэке).

## Методы

-   testing: https://travelers.testing.avia.yandex.net
-   production: https://travelers.production.avia.yandex.net

| Имя                      | Метод    | URL                                                                   | Описание                                     |
| ------------------------ | -------- | --------------------------------------------------------------------- | -------------------------------------------- |
| getTraveler              | `GET`    | `/v1/travelers/:uid`                                                  | [Ссылка](getTraveler/README.md)              |
| createOrUpdateTraveler   | `POST`   | `/v1/travelers/:uid`                                                  | [Ссылка](createOrUpdateTraveler/README.md)   |
| getPassengers            | `GET`    | `/v1/travelers/:uid/passengers`                                       | [Ссылка](getPassengers/README.md)            |
| getPassenger             | `GET`    | `/v1/travelers/:uid/passengers/:passengerId`                          | [Ссылка](getPassenger/README.md)             |
| createPassenger          | `POST`   | `/v1/travelers/:uid/passengers`                                       | [Ссылка](createPassenger/README.md)          |
| editPassenger            | `PUT`    | `/v1/travelers/:uid/passengers/:passengerId`                          | [Ссылка](editPassenger/README.md)            |
| deletePassenger          | `DELETE` | `/v1/travelers/:uid/passengers/:passengerId`                          | [Ссылка](deletePassenger/README.md)          |
| getPassengerDocuments    | `GET`    | `/v1/travelers/:uid/passengers/:passengerId/documents`                | [Ссылка](getPassengerDocuments/README.md)    |
| getPassengerDocument     | `GET`    | `/v1/travelers/:uid/passengers/:passengerId/documents/:documentId`    | [Ссылка](getPassengerDocument/README.md)     |
| createPassengerDocument  | `POST`   | `/v1/travelers/:uid/passengers/:passengerId/documents`                | [Ссылка](createPassengerDocument/README.md)  |
| editPassengerDocument    | `PUT`    | `/v1/travelers/:uid/passengers/:passengerId/documents/:documentId`    | [Ссылка](editPassengerDocument/README.md)    |
| deletePassengerDocument  | `DELETE` | `/v1/travelers/:uid/passengers/:passengerId/documents/:documentId`    | [Ссылка](deletePassengerDocument/README.md)  |
| getPassengerBonusCards   | `GET`    | `/v1/travelers/:uid/passengers/:passengerId/bonus-cards`              | [Ссылка](getPassengerBonusCards/README.md)   |
| getPassengerBonusCard    | `GET`    | `/v1/travelers/:uid/passengers/:passengerId/bonus-cards/:bonusCardId` | [Ссылка](getPassengerBonusCard/README.md)    |
| createPassengerBonusCard | `POST`   | `/v1/travelers/:uid/passengers/:passengerId/bonus-cards`              | [Ссылка](createPassengerBonusCard/README.md) |
| editPassengerBonusCard   | `PUT`    | `/v1/travelers/:uid/passengers/:passengerId/bonus-cards/:bonusCardId` | [Ссылка](editPassengerBonusCard/README.md)   |
| deletePassengerBonusCard | `DELETE` | `/v1/travelers/:uid/passengers/:passengerId/bonus-cards/:bonusCardId` | [Ссылка](deletePassengerBonusCard/README.md) |
| getDocumentTypes         | `GET`    | `/v1/document_types`                                                  | [Ссылка](getDocumentTypes/README.md)         |
