# Инструмент создания календаря

## Пример использования
```bash
wget "http://calendar.yandex-team.ru/export/holidays.xml?start_date=2019-01-01&end_date=2019-01-31&country_id=225&out_mode=all" -O region225.xml -q
wget "http://calendar.yandex-team.ru/export/holidays.xml?start_date=2019-01-01&end_date=2019-01-31&country_id=149&out_mode=all" -O region149.xml -q
./builder --files region255.xml --files region149.xml --version test --output calendar.fb
```
