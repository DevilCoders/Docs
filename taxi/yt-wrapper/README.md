# yandex-taxi-yt-wrapper

Динамическая библиотека для использовании функциональности Yt в продуктах
MLU (Yandex Taxi) с фреймворком userver.

## Ограничения
Нельзя
- возвращать/принимать классы из стандартной библиотеки, т. к. используются
  разные версии libstdc++
- выбрасывать исключения из публичных методов, т. к. используются разные
  стандартные библиотеки и компиляторы
