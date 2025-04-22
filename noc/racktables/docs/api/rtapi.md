# RTAPI
{% note alert %}

`RTAPI` больше не будет развиваться. Если у вас новый проект, лучше посмотреть в сторону [InvAPI](https://docs.yandex-team.ru/invapi). 

{% endnote %}

## Основное
RTAPI доступен для использования внутри НОК. Не требует авторизации для чтения, выполняет функции PHP напрямую из кода.

[Исходный код клиента и дока в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/noc/rtapi)
[Список разрешенных функций](https://noc-gitlab.yandex-team.ru/nocdev/racktables/blob/master/scripts/API_server.ini)

## Установка
```bash
pip3 install -i https://pypi.yandex-team.ru/simple rtapi
```
Или последнею версию из Аркадии:
```bash
pip install svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/noc/rtapi
```
