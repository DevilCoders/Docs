# hprof

Shiva предлагает автоматический сбор hprof дампов из упавших java приложений. Для этого необходимо записать hprof дамп по определенному пути, который передается в контейнер через переменную окружения [DEPLOY_HPROF_DIRECTORY](../service-preparation/service-requirements.md#_deploy_hprof_directory).
Сделать это можно к примеру, так:

```sh
${JAVA_HOME}/bin/java -XX:HeapDumpPath=${_DEPLOY_HPROF_DIRECTORY}/<filename.hprof>
```

Они доступны на странице сервиса во вкладке `hprofs`
