# Билдер календаря

Создать календарь можно следующим bash-скриптом (запускать следует из текущей папки).

```bash
start_date="2019-10-01"
end_date="2019-10-30"
xmls=""

for country_id in 225 11119 149 977 983 181
do
    wget "http://calendar.yandex-team.ru/export/holidays.xml?start_date=$start_date&end_date=$end_date&country_id=$country_id&out_mode=all" -O region$country_id.xml -q
    xmls="$xmls region$country_id.xml"
done

ya m -r
./builder --files $xmls --output calendar.fb --version test
rm $xmls
```
