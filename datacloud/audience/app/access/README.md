# Инструмент для управления доступом к сегментам
Можно выдать/оторвать доступ к отдельному сегменту или списку сегментов

### chmod
Параметры
- `--share` - выдать доступ
- `--revoke` - оторвать доступ
- `--user-id` - пользователь которму будет выдан/оторван доступ
- `--segment-id` - id сегмента
- `--filename` - имя файла со списком сегментов. Каждый сегмент в отдельной строке

Примеры

Выдать доступ к сегменту `12345` пользователю `username`
```
export AUDIENCE_TOKEN=""
./access chmod --share --user-id username --segment-id 12345
```

Оторвать доступ
```
./access chmod --revoke --user-id username --segment-id 12345
```

Выдать доступ к нескольким сегментам в файле `input.txt`
```
./access chmod --revoke --user-id username --filename input.txt
```
