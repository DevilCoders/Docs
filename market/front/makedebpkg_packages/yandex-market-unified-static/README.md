yandex-market-skubi-static
----------------

Статика для [yandex-market-skubi](https://github.yandex-team.ru/market/packages/tree/master/yandex-market-skubi).

Запускается автоматически при сборке yandex-market-skubi.

Для сборки необходимы следующие переменные окружения:

  - `PACKAGE` :: Пакет для которого собирается статика
  - `VERSION` :: Версия родительского пакета
  - `SOURCES` :: Абсолютный путь к папке с побилженными исходниками

### Сборка пакета

Этот пакет не расчитан на то чтобы собираться в одиночестве, но это может потребоваться.
Для начала нам нужен Маркет, собранный для production окружения(нам нужна его пожатая статика).

Задаём переменные окружения:

```bash
export PACKAGE='yandex-market-skubi'; # Родительский пакет, на основе этого будет вычислено имя текущего пакета
export VERSION=111;                   # Версия родительского пакета. Нужно чтобы она была уникальной
export SOURCES='/path/to/static';     # Абсолютный путь к пожатой статике Маркета. Например, в yandex-market-skubi это `/.../MarketNode/market-skubi/_`
```

Далее можно переходить к [общим инструкциям по сборке](https://github.yandex-team.ru/market/packages#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2).

### Загрузка в репозиторий

Этот пакет нужно загрузить в репозиторий [verstka](https://github.yandex-team.ru/market/packages/blob/master/README.md#verstka).

Информация о том [как загружать пакеты](https://github.yandex-team.ru/market/packages/blob/master/README.md#%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9).
