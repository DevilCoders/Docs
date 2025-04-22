# MIR
Market Indexer Runner

## Запуск как тест
```
ya make -tt test/
ya make -tt test/ --test-stderr --test-keep-symlinks --keep-temps
```

## Запуск на реальном yt кластере
```
ya make -tt --keep-temps --test-stderr -DCUSTOM_YT_PROXY_VAR=hume.yt.yandex.net -DCUSTOM_YT_TOKEN_PATH_VAR=/home/$LOGNAME/.yt/token -DCUSTOM_YT_HOME_VAR=//tmp/$LOGNAME/mir
```