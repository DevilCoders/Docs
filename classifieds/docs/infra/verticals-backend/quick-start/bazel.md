# Как пользоваться bazel

## Установка bazelisk

`bazelisk` — это специальный лаунчер, который умеет динамически загружать нужную версию bazel

{% list tabs %}

- MacOS:

   ```(bash)
   brew install bazelisk
   ```

- Linux:

   ```(bash)
   sudo curl -Lo /usr/local/bin/bazel \
      https://github.com/bazelbuild/bazelisk/releases/download/v1.11.0/bazelisk-linux-amd64
   sudo chmod +x /usr/local/bin/bazel
   ```

{% endlist %}

## Установка buildozer

`buildozer` – средство для редактирования BUILD-файлов из CLI

{% list tabs %}

- MacOS:

    ```(bash)
    brew install buildozer
    ```

- Linux: 

   ```(bash) 
   sudo curl -Lo /usr/local/bin/buildozer \
      https://github.com/bazelbuild/buildtools/releases/download/5.1.0/buildozer-linux-amd64
   sudo chmod +x /usr/local/bin/buildozer
   ```

{% endlist %}

## Настройка bazel

Рекомендуется положить в `user.bazelrc` в корне репозитория файл со следующим содержимым:

```
build -k                  # продолжить сборку даже после ошибки
test --test_output=errors # писать логи упавших тестов (по умолчанию даётся ссылка на логи)
```
