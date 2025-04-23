# Инструмент для заливки и обновления сегментов

- `--date` - дата за которую посчитан скор
- `--audience` - имя аудитории - `--file` - файл со списком аудиторий. Каждая аудитория должна быть указана на отдельной строке.

Обязательно должны быть указаны `--date` и одно из полей `--audience` либо `--file`.

Имена аудиторий можно посмотреть в таблице `//home/x-products/production/config/datacloud/audience/audience_config`

Пример
```
export AUDIENCE_TOKEN=""
./pipeline upload --audience audience_1234 --date 2020-03-17
```

Несколько сегментов
```
./pipeline upload --filename list.txt --date 2020-03-17
```
