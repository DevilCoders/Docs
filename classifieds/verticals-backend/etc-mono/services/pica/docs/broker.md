# Поставка событий в broker

События создания, скачивания, прокачки меты и удаления попадают в YT и кафку через broker.

[Модель события](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/pica/event.proto#L27)

## Где:

#### YT
Льем в ```Hahn```: ```//home/verticals/broker/{ENV}/warehouse/pica/image_log/1d```

Нарезаем по дню.
Таблицы сортируются по неймспейсу, id изображения и времени события.
Свежие таблицы могут быть неотсортированными.

- [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/test/warehouse/pica/image_log/1d)
- [Прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/pica/image_log/1d)

#### Кафка
Топик ```broker-pica-image_log```

## Гарантии

Все совершаемые с картинкой действия через пику гарантированно попадут в брокер. Гарантируем at least once.

**Важно!** Порядок записи в брокер и кафу не гарантируется. Для упорядочивания необходимо использовать timestamp события.
Использование timestamp в качестве версии не совсем честно.

В теории это может приводить к некорректной последовательности операций по разным причинам:
 - рассинхронизация времени на машинах
 - лаг между совершением записи в базу и получением текушего timestamp
 
Считаем, что на практике, такого происходить не будет. Если будет болеть - придумаем честные версии.

#### Удаления
Если по удаленному изображению попробовать его создать/прокачать заново -
изображение создастся с новым pica image id (т.к. генерим по контенту).
Соответственно, в топике получим событие удаления, затем по этому же image_id события создания/скачивания и т.д.
image name аватарницы для заново скачанных гарантированно будет отличаться.
 