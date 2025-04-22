# Требования к пакетам

В infratest на пакеты накладываются следующие ограничения:

- Версии зависимостей в пакетах должны быть выровнены. Исключения слудует вносить в [.config/common-dependencies.js](../.config/common-dependencies.js).
- Пакеты должны удовлетворять требованиям [package-checker](../packages/package-checker/README.md). Актуальную конфигурацию можно найти в [.config/package-checker.js](../.config/package-checker.js).

Для проверки всех пакетов:
- Настроить монорепо, счекаутить свежий транк, отрибейзиться.
- В корне монорепо выполнить `npm run check-packages`.
