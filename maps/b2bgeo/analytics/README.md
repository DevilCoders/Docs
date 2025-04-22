# Монорепозиторий аналитики b2bgeo

## Настройка системы

Install instructions inside folder "arcadia/maps/b2bgeo/analytics"

1. Клонировать репозиторий себе.
    ```bash
    $ arc mount -m ~/arcadia
    $ cd ~/arcadia/maps/b2bgeo/analytics
    $ arc pull
    ```

2. Настроить виртуальное окружение. Можно любым удобным способом.
    ```bash
    $ python3.8 -m venv venv
    $ . venv/bin/activate
    (venv) $ pip install -U pip
    ```

## Установка

3. Устанавливается **только под linux**.
   Подготовить машину (Нужен доступ sudo).
   На icar/dedal и большинстве других наших машинок, этот этап можно
   пропустить.
    ```bash
    sudo apt-get update
    sudo apt-get install python-dev libgdal-dev postgresql
    ```
   Для macos нужно выполнить другие команды (позже будет описано)

4. Собрать setup.py
    ```bash
    (venv) $ pip install setuptools wheel
    (venv) $ pip install -U pip
    (venv) $ pip install -i https://pypi.yandex-team.ru/simple -e .
    # Если команда вызывается не в директории YOUR_ARCADIA_HOME/maps/b2bgeo/analytics то подставьте вместо точки правильный путь.
    # Опция -e устанавливает пакет в editable-режиме, все правки файлов будут подхватываться ядром python-а, что очень удобно для отладки.
    # Для "боевой" сборки (как в кластермастере) ее не надо использовать.
    ```

### Создание ядра jupyter с нужными пакетами

5. Создать ядро jupyter и добавить его в Jupyter-сервер
    ```bash
    # ipykernel будет уже установлен, если ранее ставили tools
    (venv) $ pip install ipykernel
    # создаем новое ядро для jupyter
    python -m ipykernel install --name analytical_kernel --display-name "Python 3.8 analytics" --user
    
    # после этого рестартим айпайтон сервер
    # Зайти в Control Panel нашего Jupyter-сервера (сейчас это https://icar.sas.yp-c.yandex.net/hub/home), сделать Stop My Server и затем My Server
    
    # по идее, если мы запускаем новый кернел из-под виртуального окружения, то в настройках кернела сразу будет все правильно
    # но если вдруг не так, то идем сюда
    cd ~/.local/share/jupyter/kernels/analytical_kernel
    # и в файле kernel.json прописываем руками путь к питону как
    # "/home/dante/venv/bin/python"
    ```

### Раскладка токенов

6. Раскатываем токены:
    - Для аналитиков предпочтительно запускать без указания параметров (либо с параметром `-m user`)
       ```bash
       (venv) $ python deploy/place_tokens.py
       ```

    - Чтобы разложить токены в домашку робота, запустить с параметром `-m robot`
       ```bash
       (venv) $ python deploy/place_tokens.py -m robot
       ```

    - Для менеджеров доступна опция `-m manager`, чтобы получить минимальный набор токен для запуска некоторых скриптов.
      ```bash
      (venv) $ python deploy/place_tokens.py -m manager
      ```

## FAQ

Q: Выполняю команду, пакет не инсталлируется

A: Надо либо инкрементировать версию пакета (найти  `__version__` в коде), либо добавить к команде
флаг `--force-reinstall`. Это в свою очередь приведет к переустановке также и всх зависимостей. Если в вашей ветке нет
новых зависимостей, то можно дополнительно добавить флаг `--no-deps`, и будет установлен только сам пакет.

Q: Требует аркадийный токен при попытке смонтировать аркадию (пункт 1)

А. Нужно получить аркадийный токен и положить в нужную директорию:
Зайдите по ссылке: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5c407aafc5c242948b532842a9a07da6 и нажмите "Разрешить".
Скопируйте полученный токен в файл `~/.arc/token` или `(%USERPROFILE%\.arc\token)`:

```bash
$ echo -n AQAD-... > ~/.arc/token
$ chmod 600 ~/.arc/token
```
