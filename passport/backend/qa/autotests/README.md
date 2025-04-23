# E2E автотесты для бекендов Паспорта

## Запуск
1. (или) `./run_tests.sh`
2. (или) Создать в [Sandbox](https://sandbox.yandex-team.ru/) задачу `PASSPORT_AUTOTESTS`

### Подробнее о локальном запуске
`./run_tests.sh -h`

Например `cd passport && ../run_tests.sh`

NB: значение параметра надо передавать через пробел, а не через знак равенства. Например: `./run_tests.sh --env production`

## Linux
Скачать deb-пакет с последней версией можно с https://github.com/allure-framework/allure2/releases

Почему-то моя версия изначально не дала запустить allure никому кроме root, поэтому пришлось ещё сделать
`sudo chmod o+rx /usr/share/allure/bin/allure`

## MacOS
`brew install allure`, чтобы просматривать подробные тест-репорты

## FAQ
1. При запуске появляется ошибка `error: No keys in the SSH Agent. Check output of 'ssh-add -l' command`
    * Нужно выполнить команду `ssh-add ~/.ssh/id_rsa`
2. Как поменять/дополнить секреты?
    * [testing](https://yav.yandex-team.ru/secret/sec-01ewabcg6j4jyd129mt11t4r5d)
    * [production](https://yav.yandex-team.ru/secret/sec-01ewaz478n30zjpnknv6dsay4f)
    * [intranet testing](https://yav.yandex-team.ru/secret/sec-01ewaz5zsas0jbc2p5djtrc2sz)
    * [intranet production](https://yav.yandex-team.ru/secret/sec-01ewaz85aye7za71za8h9zyfdr)
