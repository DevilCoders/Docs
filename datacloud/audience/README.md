# Шпаргалка по заливке аудиторий

### 1. Заливаем модель

Инструмент для заливки модели лежит здесь: `arcadia/datacloud/cli/upload_model`.
Для корректной работый необходимо указать токены до YT и YQL

Параметры:
- `-p` - partner\_id, для какого партнера подготовлена модель
- `-s` - score\_name, имя скора
- `-l` - путь до pickle модели на локальной машине
- `-c` - тип модели
- `-f` - признаки
- `--transfer-off` - отключить трансфер на YDB

Пример
```
export YT_TOKEN=""
export YQL_TOKEN=""
./upload_model -p internal -s score_42 -l /home/username/local_path_to_model.pkl -c PredictProbaModel -f DSSMFeatureBase400 NormedS2VFeatureBase512 --transfer-off
```

В результате появится запись в таблице `//home/x-products/production/config/datacloud/api-models-config`.

Бинарник модели будет залит в `//home/x-products/production/datacloud/bins/partner_models`.

### 2. Применить модель

Если все правильно сделано, при следующем запуске в ClasterMaser задача `apply_models` применит модель к актуальным данным.

Если хочется ускорить процесс, можно воспользоваться лаунчером `arcadia/datacloud/launcher/app` и запустить задачу вручную.

Пример
```
./app --program apply_models
```

Таблица со скором появится в `//home/x-products/production/datacloud/models`.

### 3. Создать аудитории

Создавать и управлять аудиториями можно с помощью `arcadia/datacloud/audience/app/config`. Документация лежит рядом с утилитой.

Пример
```
./config add-audience --partner-id internal --score-name score_42 --low 0.0 --up 0.1 --audience-name audience_42 --parts 5
```

Запись о новой аудитории будет в таблице `//home/x-products/production/config/datacloud/audience/audience_config`.

### 4. Залить аудитории

Инструмент `arcadia/datacloud/audience/app/pipeline`. Документация прилагается.

Пример
```
for aud in audience_42_0-10 audience_42_10-20 audience_42_20-30 ; do ./pipeline upload --audience $aud --date 2020-03-24; done
```

Записи о залитых сегментах прорастают в таблицу `//home/x-products/production/config/datacloud/audience/segment`.

### 5. Получить id залитых сегментов и добавить в тикет

Приложение `arcadia/datacloud/audience/app/config`

Пример
```
./config list-segments --audience-name audience_42_0-10 --id-only
```

### 6. Расшарить аудитории

Для управления доступом можно использовать `arcadia/datacloud/audience/app/access`, документация в наличии.
