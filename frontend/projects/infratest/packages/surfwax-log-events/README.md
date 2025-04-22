# surfwax-log-events

В модуле лежат протобуфы событий SurfWax WebDriver Proxy поставляемые через доставку логов (UnifiedAgent → Logbroker →
LogFeller → YT).

Модуль не собирается на macOS High Sierra и ниже из-за несовместимой libc protoc.

## Build

```
$ npm i
$ npm run build
```
