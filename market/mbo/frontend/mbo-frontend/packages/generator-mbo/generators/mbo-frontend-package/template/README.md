# your-super-project

### Запуск проекта

При первом запуске приложения, в файл `/etc/hosts` (`C:\Windows\System32\Drivers\etc\hosts` - для Windows) необходимо добавить следующие записи (это необходимо сделать только один раз):

```
127.0.0.1   localhost.msup.yandex-team.ru
127.0.0.1   localhost.msup.yandex.ru
```

Далее устанавливаем зависимости:

```bash
npm ci
```

Запускаем приложение:

```bash
npm start
```
