# Скрипт сборка информации об используемых счетчиках аналитики

Соберет json, в котором будет содержаться информация об используемых счетчиках.
Встраивается через ЯБро за флагом эксперимента

Собираем данные о:
- Google Analytics
- GA 4
- Facebook
- Метрика

Формат: `{ scripts: ["ga", "ga4", "gtag", "fb", "mc"] }`

Данные отправляем через `yandex.statistics` c ключем `analytics_scripts`

Например: `yandex.statistics.send("analytics_scripts", {"scripts": ["ga", "ga4", "gtag", "fb", "mc"]})`

