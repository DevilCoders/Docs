# Обновление Alexandria на Ubuntu
[Завести работы](https://forms.yandex-team.ru/surveys/21525/)  
[Пример тикета](https://st.yandex-team.ru/NOCRFCS-6055)

## Сборка
* Сборка осуществляется через [CI Arcadia](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Falexandria&id=alexandria-release)
* Параметры [CI Flow](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/a.yaml)


## Установка
#### Установка пакета
Установка пакета осуществляется через [Кондуктор](https://c.yandex-team.ru/)

[Пакет Alexandria](https://c.yandex-team.ru/packages/alexandria) устанавливается последовательно на 
* [prestable](sas-rt-prestable1.net.yandex.net)
* [stable](man1-rt1.yndx.net)

[Проверить доступные версии пакета](http://dist.yandex.net/find?pkg=alexandria).

В тикете на раскатку указывается версия в формате "1.0.0.{svn_revision}". 
> Underscore("_") не пройдёт этап debuild при сборке в CI.

#### Перезапуск сервиса: 
```bash
sudo systemctl stop alexandria
sudo systemctl start alexandria
sudo systemctl status alexandria
```

#### Проверка Syslog: 
```
sudo journalctl -eu alexandria
/var/log/syslog
```

## Изменение настроек
### Настройки Alexandria:  
`/etc/alexandria/alexandria.yaml`

{% note info %}

Для применения настроек может понадобиться "sudo /etc/init.d/nginx reload"

{% endnote %}

### Настройки php-fpm Racktables:  
```
git@noc-gitlab.yandex-team.ru:nocdev/configs.git
/usr/local/configs/php-fpm/rt.conf
```

{% note info %}

Адрес сервера Alexandria для sw-ver-report определяется переменной "env[ALEXANDRIA_URL]", по умолчанию localhost.

{% endnote %}