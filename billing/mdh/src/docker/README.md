## Docker для локального запуска

Из директории проекта:

```
docker build -f src/docker/Dockerfile . --tag mdh
docker run --rm -p 8000:8000 --name mdh-server mdh
```

* Админ: http://localhost:8000/admin
* UI API: http://localhost:8000/uiapi
