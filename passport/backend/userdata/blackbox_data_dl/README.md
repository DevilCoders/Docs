## cmd/bb-dl

### Описание конфига на файловой системе
```
[tvm]
api_url=урл до tvm-демона
auth_token=токен для подключения к tvm-демону
src=какой src использовать в тикете

[blackbox]
api_url=урл до ЧЯ
dst=tvm id ЧЯ
```

### Как добавить колонку
1. Поправить запрашиваемые атрибуты в `datamap.go`
2. Поправить сохраняемые атрибуты в `export.go`
3. `export PATH=$GOROOT/bin:$PATH`
4. `ya make ~/gopath/src/a.yandex-team.ru/vendor/github.com/mailru/easyjson/easyjson`
5. `GOPATH=~/gopath ~/gopath/src/a.yandex-team.ru/vendor/github.com/mailru/easyjson/easyjson/easyjson datamap.go`
