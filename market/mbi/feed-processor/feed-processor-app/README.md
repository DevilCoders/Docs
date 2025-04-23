## Feed-Processor
Описание компонента: https://wiki.yandex-team.ru/mbi/newdesign/components/Feed-Processor/

## Разработка
### Локальный запуск:
0. Генерируем проект feed-processor-app
1. Запускаем postgresql:
   1. Либо через Docker Compose. В директории проекта в аркадии `docker-compose up -d`
   2. Либо через IDEA заходим в файлик `docker-compose.yml` и стартуем его через зеленый треугольник
2. Создаем конфигурацию для запуска в IDEA
   1. Точка старта - `FeedProcessor`
   2. Добавляем VM options: `-Dspring.profiles.active=development,local`
   3. Добавляем `YAV_TOKEN` в Environment variables. Токен можно получить тут: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982

**Готово. Приложение запущено!**

### Возможно, для работы вам понадобится:
1. Создать динамические таблицы для своего аккаунта.
   1. Для этого надо запустить приложение.
   2. Подключиться по теленту к tms консоли `telnet localhost 36032`
   3. Вызвать команду `init-yt-dynamic-table TABLE_NAME`. Вместо `TABLE_NAME` подставь название нужной таблицы. Список возможных значений тут: `ru.yandex.market.mbi.feed.processor.parsing.yt.DynamicTable`
   4. Подтверждаем действие вводом `yes`

### Troubleshooting:
1. Не удалось подключиться к YAV
   1. Проверь, есть ли у тебя права к Секретнице: https://yav.yandex-team.ru/secret/sec-01fj3hhj4xxj4ce7sb53j8qzxr/explore/versions
   2. Если прав нет, запросить можно у MBI Devops
2. Отключить поход в YAV за секретами
   1. Для отключения надо добавить VM Options: `-Dyav.local.disabled=true`
