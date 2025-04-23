# Установка окружения
1. Скачиваем скрипт и распаковываем в любое удобное место
2. Скачиваем [**Python3**](https://www.python.org/getit/) или устанавливаем при помощи **Homebrew** командой `brew install python3`
3. Устанавливаем **Python3** добавив во время установки чекбокс **Add python to PATH** (чтобы не нужно было каждый раз прописывать полный путь к питону в терминале) - если питон уже установлен - оставляем текущую версию  - можно проверить набрав в консоли `python -V`
4. Устанавливаем **pip** - набрав в консоли `sudo easy_install pip`
5. Устанавливаем библиотеку **requests** командой в терминале `pip3 install requests`
6. Устанавливаем библиотеку yaml `brew install libyaml` and  then `sudo python -m easy_install pyyaml`
7. Устанавливаем библиотеку yandex-yt командой в терминале `pip3 install -i https://pypi.yandex-team.ru/simple/ yandex-yt`
8. Устанавливаем клиент ST командой в терминале `pip3 install -i https://pypi.yandex-team.ru/simple/ startrek_client`


### Благодарности
Сделано на базе существующих скриптов:

https://github.yandex-team.ru/plakhov/am_asessors_script - спасибо Андрею @plakhov!
https://wiki.yandex-team.ru/users/adidkovskaya/assessorsscript/ - спасибо Анжелике @adidkovskaya!
Спасибо Кате @kateogar!

