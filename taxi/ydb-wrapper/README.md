# yandex-taxi-ydb-wrapper

Динамическая библиотека для использовании функциональности YDB в продуктах
MLU (Yandex Taxi) с фреймворком userver.

## Ограничения
Нельзя
- возвращать/принимать классы из стандартной библиотеки, т. к. используются
  разные стандартные библиотеки C++ и компиляторы
- выбрасывать исключения из публичных методов, т. к. используются разные
  стандартные библиотеки C++ и компиляторы
