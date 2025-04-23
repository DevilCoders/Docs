# Taxi's Infrastructure debian packages

## Воспроизводимость и герметичность сборки

-   мы не пиним версии debian depends потому что скрипты работают в негерметичном окружении и нам нормально не гарантировать их запуск

-   мы нежестко пиним build depends (>= (дополнительно, опционально, <=)) чтобы создать условно-воспроизводимое окружение для сборки

-   софт работающий в контейнерах или собираемый через pip обязан пинить все критически-важные для работы зависимостей пакеты

## Как работать с пакетами локально

### Сборка в контейнере

Важная особенность - все команды работы с arc в контейнере могут **не** работать по причине отсутствия на момент 31.03.2021 поддержки user_xattr в монтируемом диске, если arc команда "зависнет", необходимо ее прерывать через однократное нажатие ctrl-C (https://st.yandex-team.ru/DEVTOOLSSUPPORT-7372)

```bash
# скрипт подразумевает, что структура папок сделана по обучению из arcadia starter guide,
# у пользователя установлен ya и токен экспортирован в ~/.ya_token командой ya whoami --save-token
./run_build_container_local.sh xenial

# мы внутри контейнера! проверяем что пакет устанавливается и все работает как должно
/arc/arcadia/ya package --arch-all --debian --not-sign-debian packages/examples/hello-world/hello_package.json

tar xvf hello-package.1.0.tar.gz

apt install -f ./hello-package_1.0_amd64.deb

```

### Работа с питон-проектами

```bash
cd taxi-ping-handle-monitoring
poetry env use 3.9.2
poetry install
```

## CI

### Who is this guy robot-taxi-ops-deb

[Управляет CI этот робот](https://staff.yandex-team.ru/robot-taxi-ops-deb)

### Секреты

yandex.vault: - https://yav.yandex-team.ru/secret/sec-01f1csk3bq55axyz00psmjg2q8/explore/versions
sandbox.vault: - robot-taxi-ops-deb-ssh (plain text) - robot-taxi-ops-gpg-private (base64) - robot-taxi-ops-gpg-public (base64)

Пароль:

-   https://yav.yandex-team.ru/secret/sec-01f10tv4a8xs5gmea9ghacgjrh/explore/versions

### TODO

-   try tutorial app with xterm.js
-   move local dockerfile building to ya package

### Примеры

-   https://a.yandex-team.ru/arc/trunk/arcadia/devtools/dummy_arcadia/package
