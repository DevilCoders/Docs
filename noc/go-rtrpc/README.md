# Ахтунг!
Либа предназначена для использования строго внутри NOC.
Использовать на свой страх и риск, багов много. Или нет.

## Примеры
### Просто
```go
rt, err := NewRTClientDefaultRO()
if err != nil {
    panic(err)
}
v, err := rt.SpotEntity("object", 2485)
if err != nil {
    panic(err)
}
ok, err := rt.AutoConsiderGivenConstraint(v, "{сервер RT}")
if err != nil {
    panic(err)
}
fmt.Println(ok)
```

### Чуть сложнее
```go
rtaddr := ""
if rtapiHost, ok := os.LookupEnv("RTAPI_CONF_SERVER"); ok {
    rtaddr = rtapiHost
}
if rtapiPort, ok := os.LookupEnv("RTAPI_CONF_PORT"); ok {
    rtaddr += ":" + rtapiPort
}
if rtaddr == "" {
    rtaddr = "ro.racktables.yandex-team.ru:8036"
}
rt, err := gortrpc.NewRTClient("tcp+ssl", rtaddr, "gorttest")
if err != nil {
    panic(err)
}
```
