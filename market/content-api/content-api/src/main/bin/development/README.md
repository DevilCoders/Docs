Как запустить на dev сервере
====

1. Собираем тарник с капи командой из папки market/content-api/content-api
```shell
   ya package make/pack/package.json --target-platform=default-linux-x86_64
   ```
2. Положить получившийся архив на дев сервер
```shell
   scp <archive> aida:<home_dir>
   ```
3. Развернуть получившийся архив
4. В папке bin/development запустить start-development.sh:
```shell
   ./start-development.sh -p <port> -d <debug_port> -t <file_with_tvm_key>
   ```
где port - порт, на котором будет развернуто приложение
    debug_port - дебаг порт
    file_with_tvm_key - файл, в котором лежит твм секрет капи для тестинга (рекомендуется создавать этот файл с r/w правами только для овнера)
