# yandex-ansible-pull

[Примеры](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dyandex-ansible-pull%26(namespace%3Ddirect.prod%7Cnamespace%3Ddirect.test%7Cnamespace%3Ddirect.dev)) проверок.

## Описание { #description }
Проверяет, что yandex-ansible-pull успешно дорабатывает до конца.  
Поломка ее не является критичной проблемой, но потенциально может вызвать не работу всяких приложений.

## Диагностика { #diagnostics }
### Вариант 1
Посмотреть лог `/var/log/yandex-ansible-pull/ansible.log` на сервере.

### Вариант 2
Запустить руками yandex-ansible-pull и посмотреть его вывод:
```sh
yandex-ansible-pull
```

## Подробности { #details }
yandex-ansible-pull — программа, которая готовит машину к работе (устанавливает пакеты, настраивает и запускает демона).

Принцип работы — запускается ansible-pull, он скачивает из репозитория плейбук и применяет его к текущему хосту.
В результате хост приводится в состояние, описанное конфигурацией плейбука (зависит от имени хоста, кондукторных групп и прочего).

{% note info %}

Используется не master-ветка. В зависимости от ДЦ — это **ansible-pull-stable** или **ansible-pull-limtest**.

{% endnote %}

Запускается по крону в начале каждого часа.

## Ссылки { #links }
- [репозиторий с плейбуками](https://github.yandex-team.ru/DirectAdmin/ansible-playbooks)
- [исходники yandex-ansible-pull](https://github.yandex-team.ru/DirectAdmin/yandex-du-ansible-pull)
