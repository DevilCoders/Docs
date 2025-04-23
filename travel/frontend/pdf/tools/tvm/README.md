## Конфигурирование tvm с помощью скриптов

### 0. Установка yav

Консольная утилита **yav** поможет рабработчикам и системным администраторам получать, создавать и обновлять секреты в [Секретнице](https://vault-api.passport.yandex.net/docs/).

1. Установите python3 и pip3 на **свой компьютер**, например [инструкция Mac](https://medium.com/swlh/installing-python-and-pip-on-mac-72b7639a58).

2. Установите **yav**

```
pip3 install yandex-passport-vault-client -i https://pypi.yandex-team.ru/simple
```

### 1. Создание tvmtool.conf

На **своем компьютере**:

```
cd tools/tvm

sh create.sh
```

Скрипт получит секрет и создаст tvmtool.conf из шаблона tvm.blank.json, который добавлен в gitignore.
Далее доставьте файл на **dev-машину** вашим средством синхронизации (например rsync)

### 2. Deploy файлов

На **dev-машине**:

```
cd tools/tvm

# скопируйте сгенерированный конфиг в папку с настрйоками tvm
sudo cp tvmtool.conf /etc/tvmtool/tvmtool.conf
sudo cp local.auth /var/lib/tvmtool/local.auth

# перезапустите tvm
sudo service yandex-passport-tvmtool restart
```

### Переключение между проектами

Когда на одной dev-машине разрабатываются несколько приложений с разными tvm конфигурациями.
Для переключения между проектами достаточно выполнить скрипт из 2 шага.
