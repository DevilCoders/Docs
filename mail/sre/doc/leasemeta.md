### Что делает сервис
Распределенный лок-сервер, позволяет клиентам брать временные локи на ресурсы.
Основные клиенты: xeno, collectors, equalizer - используют сервис для захвата шардов почтовой метабазы.
Xivahub - хранит метаданные кластера.

### Импакт на пользователей от отключения сервиса
Клиенты не могут брать локи.
Последствия для xivahub - перестают ходить пуши.
В общем случае, обработка недоступности сервиса реализуется на стороне клиента.

### Импакт остановки тачки/ДЦ
Кворум N/2+1.
Для инсталляции из 5 инстансов может быть недоступно до 2 инстансов.
Для инсталляции из 3 инстансов может быть недоступен 1 инстанс.

### Особенности деплоя
Деплоим строго по одной тачке.
В окружении production инстансы сервиса прибиты гвоздями к хостам с помощью qloud storages.
Рецепт починки стораджей: https://wiki.yandex-team.ru/rtec/oncall/lease/#kakpochinitstoragevqloud

### Критичные метрики
Следим за общими для SRE сервисов метриками: cores, ephemeral.

### Куда ходит
Бэкендов у сервиса нет.
