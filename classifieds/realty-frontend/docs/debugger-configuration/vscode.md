# Настройка дебаггера для VSCode

Нужнно доабвить в файл запись `.vscode/launch.json`:

```json
{
    "type": "node",
    "request": "attach",
    "name": "Attach to Process",
    "port": 9229,
    "remoteRoot": "/home/<username>/www/<folder-name>/realty-www",
    "localRoot": "${workspaceRoot}/realty-www"
}
```

где:
- port - порт дебаггера на **локальной машине**
- localRoot - путь до проекта на **локальной машине**
- remoteRoot - путь до проекта на **удаленной машине**

В итоге launch.json может выглядеть так:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "attach",
            "name": "Attach to Process",
            "port": 9229,
            "remoteRoot": "/home/<username>/www/<folder-name>/realty-www",
            "localRoot": "${workspaceRoot}/realty-www"
        }
    ]
}
```

Дальше можно запускать debug-сессию через вкладку с жуком или F5.
