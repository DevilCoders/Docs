## Дукалис
поможет расследовать судьбу ваших офферов и картинок.

### offer_diagnostics - инструмент для быстрого определения статуса оффера.

Позволяет получить отчет следующего вида
* [краткий](https://jing.yandex-team.ru/files/baggins/Spectacle.h19720.png)
* [может быть развернут до более подробного - с источниками данных и подробностями проверок](https://jing.yandex-team.ru/files/baggins/Spectacle.J28116.png)

#### Как запустить

```
./offer_diagnostics --help
```

```
./offer_diagnostics --feed-id 1069 --offer-id 1 --yql-token-path ~/.yql/token > out.html
```
```
./offer_diagnostics --ware-md5  --yql-token-path ~/.yql/token > out.html
```
можно не указывать путь до токена, а сделать `export YQL_TOKEN=[ваш токен]`

#### Особенности
* Работает около 5 минут (выполняются yql-запросы)
* [Описание от Вани baggins](https://wiki.yandex-team.ru/users/baggins/Kuda-propal-krasnyjj-ofer/)
* [Тикет про развитие инструмента](https://st.yandex-team.ru/MARKETINDEXER-30790)
---
### picture_diagnostics - инструмент для быстрого определения статуса картинки.

Позволяет получить отчет такого вида
* [краткий отчет о картинке](https://jing.yandex-team.ru/files/thesonsa/Снимок%20экрана%202019-10-21%20в%2011.23.44.png)
* [можно развернуть до подробного](https://jing.yandex-team.ru/files/thesonsa/Снимок%20экрана%202019-10-21%20в%2011.24.13.png)

#### Как запустить

* проверить только картинку
```
./picture_diagnostics --yql-token-path ~/.yql/token --url=https://www.mir-shapok.ru/spec/spec15503-1-3046304.jpg > out.html
```
* проверить картинку и собрать статистику по другим картинкам этого домена
```
./picture_diagnostics --yql-token-path ~/.yql/token --url=https://www.mir-shapok.ru/spec/spec15503-1-3046304.jpg --check-domain > out.html
```
* можно не указывать путь до токена, а сделать `export YQL_TOKEN=[ваш токен]`
