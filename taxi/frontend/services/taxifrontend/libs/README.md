## libs

### geoareas-fallback

Используется для вычисления центра гео-зон, которые необходимы для middleware/geolocationZone.
> TODO: Оторвать после решения задачи TAXIBACKEND-6750

**Как использовать**

выгружаем зоны из админки в файл
```bash
curl https://tariff-editor.taxi.yandex-team.ru/api/get_geoareas/?geoarea_type=tariff > libs/geoareas-fallback/__geoareas.json
```

запускаем скрипт
```bash
node ./libs/geoareas-fallback
```

### bunker-fallback

Используется при сборки для выгрузки бункера в пакет. Используется на случай если бункер не ответил.

**Как использовать**

```bash
npm run bunkerFallback
```

### tariff-map

Используется для обновления карты тарифов

**Как использовать**

выгружаем зоны из админки в файл
```bash
curl https://tariff-editor.taxi.yandex-team.ru/api/get_geoareas/?geoarea_type=tariff > libs/tariff-map/__geoareas.json
```

запускаем скрипт
```bash
node ./libs/tariff-map
```

### monitoring

Проверка доступности сервиса путём опроса роутов 
