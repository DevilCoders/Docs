# Realtime jams

A good starting point for learning about the library is [wiki](https://wiki.yandex-team.ru/users/ygorishniy/doc-realtime-jams)

## How to update default config

Upload files `engine_config.json` and `matrixnet.info` to sandbox, update `data/sandbox.inc` resource id.  
Note, there're two targets:  
  * [`data`](data) — target with library, containing default config
  * [`data/download`](data/download) — target, downloading default config; used to include into docker package. May be also useful if you want to take a look at config.
