# Развёртывание приложения

1. Для установки в virtualenv нужно указывать: pip install -i https://pypi.yandex-team.ru/simple/
2. PARAMICO
brew install libsodium
pip install -i https://pypi.yandex-team.ru/simple/ paramiko --global-option=build_ext --global-option="-L/usr/local/opt/openssl/lib" --global-option="-I/usr/local/opt/openssl/include"
echo ". $(pwd)/ver.sh" >> ~/.bashrc

# Инструкция по релизу админки запчастей

0. Если выкатывается статика, то в settings.py поменять значение STATIC_VERSION
1. Обновить версию в CHANGELOG.md
2. Выкатить в тимсити https://teamcity.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_YandexVertisAutopartsAdmin_YandexVertisAutopartsAdmin (сборка может автоматом подтянуться, но я обычно нажимаю run, чтобы побыстрее в очередь на выкатку попасть)
3. Выкатить на прод в дженкинсе https://j.vertis.yandex-team.ru/job/Deploys/job/Autoparts/job/production/job/yandex-vertis-autoparts-admin/ через "Build with Parameters" (в app_version указать версию админки нужную, в message можно что угодно указывать, лучше сообщение из чейнджлога)
