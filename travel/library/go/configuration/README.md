# Configuration
Библиотека travel/library/go/configuration является тонкой оберткой над https://github.com/heetch/confita и предлагает:
  - функцию конструктор типового лоадера конфигурации: NewDefaultConfitaLoader
  - соглашения по местонахождению и формату файлов конфигурации: /app/config.testing.yaml для тестинга и /app/config.production.yaml для прода.

## Порядок применения конфигурации
Ищет ключи в трех бекендах в следующем порядке:
1. переменные окружения
2. yaml файл (если существует файл с конфигом)
3. флаги
4. default значения

## Yaml
Yaml файлы с конфигурацией должны лежать в 
+ testing: `app/config.testing.yaml`
+ production: `app/config.production.yaml`

##Example
```
configLoader := configuration.NewDefaultConfitaLoader()
config := Config{}
_ = configLoader.Load(context.Background(), &config)
```

## Как описывать конфиги

Пусть у нас есть такая иерархия конфигов:
```go
type HTTPServerConfig struct {
    Addr string `config:"http-addr,required"`
}
type GRPCServerConfig struct {
    Addr             string `config:"grpc-addr,required"`
    EnableReflection bool
}
type Config struct {
    SomeUselessParam    string `config:"someuselessparam,required"`
    Http                HTTPServerConfig
    Grpc                GRPCServerConfig
}
defaultHttpConfig = {
    Addr: "[::]:9000"
}
defaultGrpcConfig = {
    Addr: "[::]:9001"
}
defaultConfig = {
    SomeUselessParam: "foo"
    Http:             defaultHttpConfig
    Grpc:             defaultGrpcConfig
}
```
Тогда полная yaml конфигурация будет выглядеть так:
```yaml
someuselessparam: "foo"
http:
    addr: "[::]:9000"
grpc:
    addr: "[::]:9001"
    enablereflection: false
```
Можно будет передавать параметры через переменные окружения:
```sh
SOMEUSELESSPARAM=foo GRPC_ADDR=[::]:9001 HTTP_ADDR=[::]:9000 ./executable
```
Или через флаги:
```sh
./executable -grpc-addr=[::]:9001 -http-addr=[::]:9000 -someuselessparam=bar
```

Важно помнить, что иерархия yaml должна в точности повторять иерархию ваших конфигов. При этом, по умолчанию, параметры конфигурации нельзя указывать через флаги и/или переменные окружения. Для того, чтобы это можно было сделать - нужно пометить соответствующие поля структур конфигов при помощи тэгов `config:"paramname"`.

**Правила именования**
В тэгах следует именовать переменные в кебаб-кейсе, где "-" разделяются уровни иерархии (в теории их можно именовать как угодно, но если следовать соглашению с кебаб-кейс - набор флагов становится более предсказуемым и меньше шансов случайных конфликтов). Например для Config.Grpc.Addr тэг будет `config:"grpc-addr"`, а для Config.SomeUselessParam - `config:"someuselessparam"`. Для флага grpc-addr - будет работать переменная окружения grpc_addr или GRPC_ADDR. Следует так же помнить, что тэги не имеют ничего общего с иерархией и живут в одном пространстве, а значит поля нельзя помечать одинаковым тэгом (например "addr"), даже если это поля разных структур.

**Совет**
Для дебага полезно убирать дефолтные значения. Тогда приложение может начать ругаться в тех местах, где nil value его не устроят.

## Links
https://github.com/heetch/confita
