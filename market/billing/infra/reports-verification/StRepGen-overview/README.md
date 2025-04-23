## Простая сверка отчетов по реализации товаров

Скрипты, чтобы скачать из S3 два набора отчетов по реализации товаров и сравнить итоговые суммы и количества в них.

Логика "откуда скачивать отчеты -- в download.sh"

## Пример использования

```
# получаем список id поставщиков
curl https://paste.yandex-team.ru/5820915/text >list.txt

# каталоги под скачанные отчеты
mkdir -p data/yt data/db
rm -f data/db/* data/yt/*

# скачать отчеты
cat list.txt |sed -e 's/\r//' |while read id; do ./download.sh $id; done

# сравнить
# Сравить только часть отчетов (head, tail); если список полный и все сказалось, то head и tail надо убрать
cat list.txt |sed -e 's/\r//' |head -n 301 |tail -n+2 |while read id; do echo data/db/$id.db.xlsx data/yt/$id.yt.xlsx; done |./compare-StRep.py | tee result
# или можно идти от скачанных файлов:
ls data/db |sed 's/\..*//' |while read id; do echo data/db/$id.db.xlsx data/yt/$id.yt.xlsx; done |./compare-StRep.py | tee result

# отчет загрузить на paste
ya paste result

# статистика по OK/FAIL и видам расхождений
cat result |grep -E -o '([^ ]* differ|OK)' |sort |uniq -c |sort -nr
```

