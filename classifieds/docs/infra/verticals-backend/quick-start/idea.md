# Как импортировать проект в IDEA

1. Установить плагин Bazel из Jetbrains plugin marketplace. Плагины выходят с запозданием относительно самой Intelij IDEA, поэтому перед обновлением рекомендуется проверить, есть ли совместимый Bazel-плагин. Также может быть полезным подключить [бета-канал](https://plugins.jetbrains.com/plugins/list?channel=beta) для плагинов.

2. В настройках плагина поменять путь до бинарника `bazel`:
![settings](settings.jpeg)
3. `File` -> `Import Bazel Project...`
4. Выбрать в поле `Workspace` корень репозитория, нажать `Next`.
5. Выбрать `Import project view file`, файл `.bazelproject` в корне репозитория, нажать `Next`.
6. Нажать `Finish`.

После этого IDEA должна сама запустить `Sync Project with BUILD Files`.
Этот экшн можно запускать вручную для полной пересинхронизации проекта.
Если требуется обновить только часть, достаточно нажать на нужную директорию правой кнопкой мыши и выбрать `Partial Sync ...`. Такой способ сильно быстрее полной синхронизации. 

[Документация плагина](https://ij.bazel.build/docs/bazel-plugin.html), в том числе описание экшнов.

## Поддержка scala плагинов

Чтобы идея корректно понимала код, написанный с учетом scala-плагинов (kind-projector и better-monadic-for) и не краснила код,
необходимо создать файл `./.ijwb/.idea/scala_compiler.xml` со следующим содержимым.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project version="4">
  <component name="ScalaCompilerConfiguration">
    <plugins>
      <plugin path="$USER_HOME$/Library/Caches/Coursier/v1/https/artifactory.yandex.net/public/org/typelevel/kind-projector_2.13.6/0.13.2/kind-projector_2.13.6-0.13.2.jar" />
      <plugin path="$USER_HOME$/Library/Caches/Coursier/v1/https/artifactory.yandex.net/public/com/olegpy/better-monadic-for_2.13/0.3.1/better-monadic-for_2.13-0.3.1.jar" />
    </plugins>
  </component>
</project>
```

Пути приведены для macos, на других операционных системах они могут отличаться.

Этот файл не удаляется при синхронизации проекта, поэтому о нем можно забыть до появления новых плагинов.

## Запуск zio-test из Idea

По умолчанию Idea не запускает отдельные спеки zio-тестов, только весь таргет целиком.
Для того, чтобы это стало возможно, необходимо:

1. добавить в `Plugin Repositories` репозиторий `https://bazel-build.s3.mds.yandex.net/plugins/updatePlugins.xml`.
2. установить плагин `bazel-zio-test`.
