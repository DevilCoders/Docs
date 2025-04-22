# Микроформаты Маркета
Общая документация по всем сущностям, встречающимся в компонентах Маркета.

## Цель
Систематизировать знания о форматах путём выделения и унификации сущностей, используемых при взаимодействии компонентов огромной системы Маркет между собой.

# Алгоритм внесения изменений
1. Добавляем или вносим изменения в существующий формат в отдельной ветке
2. Если добавляем новый шаблон, то создаем файлы `%microformat_name%.json` и `%microformat_name%.sample.json` с json-схемой и примером микроформата соответственно.
3. Обязательно проверяем, что `sample.json` валиден схеме. Инструкция ниже
4. Создаем PR с коммит-мессаджем таска, в рамках которого происходят изменения.
5. Ждём ревью и вливания. 
6. Время реакции на PR до **3 дней**. При возникновении проблем - пишите @camaro, @hunmar, @polyakovda

Если у вас возникают проблемы с внесением изменений в json-схему, то возможен вариант влития PR без неё. Для этого необходимо договориться с @camaro или @hunmar и создать issue вида `Дописать json-схему для %того-то%`

# JSON schema
## Gulp
Установите gulp:

> Используйте nvm для установки инструментов "глобально".

```console
npm install -g gulp
```

#### Примеры
* Небольшая сессия от @corpix доступна на [gist](https://github.yandex-team.ru/gist/corpix/140d5ef090cf44e3d631).

### fake
Генерирует JSON с фейковыми данными на основе указанной схемы.

Пример использования:
```console
~/workspace/microformats $ gulp fake -f price/price.json
[14:00:46] Using gulpfile ~/workspace/microformats/gulpfile.js
[14:00:46] Starting 'fake'...
[14:00:46] Finished 'fake' after 65 ms
{
  "price": {
    "currency": "ut sed ",
    "value": 46940439.14787471,
    "discount": {
      "oldMin": 40722862.30511963,
      "percent": -30135446.321219206,
      "isBestDeal": false
    }
  }
}
~/workspace/microformats $ gulp fake -f price/price.json --silent > price/price.sample.json
```

> В последнем вызове флаг `--silent` нужен потому что gulp выводит свой лог в stdout, а мы не хотим видеть его лог в нашем JSON файле.
> К сожалению, важно чтобы флаг был в самом конце, иначе он будет интерпретирован не правильно.

### validate
Производит валидацию данных в соответствии со схемой.

Поддерживает следующие источники данных:
* file
* url

Пример вызова:
```console
~/workspace/microformats $ gulp validate -h
[14:01:11] Using gulpfile ~/workspace/microformats/gulpfile.js
[14:01:11] Starting 'validate'...
../../.nvm/versions/node/v4.4.2/bin/gulp validate [args]

Options:
  --file, -f    JSON file with data
  --url, -u     JSON data url
  --schema, -s  JSON schema file
  --help, -h    Show help  [boolean]

~/workspace/microformats $ gulp validate -f price/price.sample.json -s price/price.json
[14:01:24] Using gulpfile ~/workspace/microformats/gulpfile.js
[14:01:24] Starting 'validate'...
[14:01:24] Finished 'validate' after 58 ms
price/price.sample.json is valid
~/workspace/microformats $ gulp validate -u http://127.0.0.1:8000/price/price.sample.json -s price/price.json
[14:01:37] Using gulpfile ~/workspace/microformats/gulpfile.js
[14:01:37] Starting 'validate'...
[14:01:37] Finished 'validate' after 63 ms
http://127.0.0.1:8000/price/price.sample.json is valid
~/workspace/microformats $ cat price/price.sample.json
{
  "price": {
    "currency": "deserunt",
    "value": 28446157.043799758,
    "discount": {
      "oldMin": -95968335.96006036,
      "percent": 5682952.00355351,
      "isBestDeal": false
    }
  }
}
~/workspace/microformats $ cat price/price.sample.json | grep isBest
      "isBestDeal": "false"
~/workspace/microformats $ gulp validate -u http://127.0.0.1:8000/price/price.sample.json -s price/price.json
[14:02:34] Using gulpfile ~/workspace/microformats/gulpfile.js
[14:02:34] Starting 'validate'...
[14:02:34] Finished 'validate' after 78 ms
There was an error while trying to validate http://127.0.0.1:8000/price/price.sample.json with price/price.json:
JSON file key /price/discount/isBestDeal does not match schema rule at /properties/price/properties/discount/properties/isBestDeal/type
Invalid type: string (expected boolean)
~/workspace/microformats $ cat price/price.sample.json | grep isBest
      "isBestDeal": false
~/workspace/microformats $ gulp validate -u http://127.0.0.1:8000/price/price.sample.json -s price/price.json
[14:03:06] Using gulpfile ~/workspace/microformats/gulpfile.js
[14:03:06] Starting 'validate'...
[14:03:06] Finished 'validate' after 64 ms
http://127.0.0.1:8000/price/price.sample.json is valid
```
