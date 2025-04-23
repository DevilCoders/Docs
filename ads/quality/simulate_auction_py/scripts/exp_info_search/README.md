### exp_info_search

Тулза для просмотра дефолта AB-шницы в виде таблицы

### Подготовка к использованию

- Сладываем JSON из ссылки https://ab.yandex-team.ru/api/v1/bigb/default в файлик `default.json`
- Собираем тулзу с помощью `ya make -r`

### Примеры

Посмотреть подмножество строчек по фильтрам

`cat default.json | ./exp_info_search CTR | tabgrep 'tabgrep '$ExpGroupID == 1 && $TypeID == 1 && $RegionID == 0' | tabpp -f | less -SR`

Команда принимает единственный аргумент - вид параметров, вроде `CTR`, `BidCorrection`, `BroadMatch` и так далее.
На выход распечатывается плоский список всех записей про этот вид параметров, найденных внутри записей `CtrPredictionParameters`.
Никаких мерджей параметров не делается, просто выдаются все строчки. Добавлены две служебные колонки, позволяющие узнать
адрес строчки в исходной JSON-структуре. `BSParametersRecordID` - номер элемента в списке BSParameters,
`RecordID` - номер элемента в структуре параметров соответствующего типа.


<table>
<tr><th> BSParametersRecordID </th><th> Priority </th><th> ExpGroupID </th><th> PageLabel </th><th> RecordID </th><th> TypeID </th><th> AuctionType </th><th> PageNo </th><th> RegionID </th><th> ProductType </th><th> Timetable </th><
<tr bgcolor="#f0f0f0"><td> 60 </td><td> 1 </td><td> 1 </td><td> None </td><td> 0 </td><td> 1 </td><td> UNSTABLE </td><td> None </td><td> 0 </td><td> None </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td
<tr><td> 60 </td><td> 1 </td><td> 1 </td><td> None </td><td> 0 </td><td> 1 </td><td> STABLE </td><td> None </td><td> 0 </td><td> None </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.1 </td><td> 2.5
<tr bgcolor="#f0f0f0"><td> 60 </td><td> 1 </td><td> 1 </td><td> None </td><td> 0 </td><td> 1 </td><td> ANY </td><td> None </td><td> 0 </td><td> None </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.1
<tr><td> 60 </td><td> 1 </td><td> 1 </td><td> None </td><td> 1 </td><td> 1 </td><td> AUCTION </td><td> None </td><td> 0 </td><td> None </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.1 </td><td> 2.5
<tr bgcolor="#f0f0f0"><td> 269 </td><td> -3 </td><td> 1 </td><td> None </td><td> 15 </td><td> 1 </td><td> AUCTION </td><td> 1 </td><td> 0 </td><td> 1 </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.
<tr><td> 269 </td><td> -3 </td><td> 1 </td><td> None </td><td> 16 </td><td> 1 </td><td> UNSTABLE </td><td> 1 </td><td> 0 </td><td> 1 </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.1 </td><td> 2.5 <
<tr bgcolor="#f0f0f0"><td> 269 </td><td> -3 </td><td> 1 </td><td> None </td><td> 16 </td><td> 1 </td><td> UNSTABLE </td><td> 2 </td><td> 0 </td><td> 1 </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0
<tr><td> 269 </td><td> -3 </td><td> 1 </td><td> None </td><td> 16 </td><td> 1 </td><td> STABLE </td><td> 1 </td><td> 0 </td><td> 1 </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.1 </td><td> 2.5 </t
<tr bgcolor="#f0f0f0"><td> 269 </td><td> -3 </td><td> 1 </td><td> None </td><td> 16 </td><td> 1 </td><td> STABLE </td><td> 2 </td><td> 0 </td><td> 1 </td><td> None </td><td> 0.1 </td><td> 1 </td><td> 0.01 </td><td> 2.5 </td><td> 0.1
</table>


