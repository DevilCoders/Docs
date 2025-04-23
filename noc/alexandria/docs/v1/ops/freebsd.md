# Обновление Alexandria на FreeBSD
[Завести работы](https://forms.yandex-team.ru/surveys/21525/)  
[Пример тикета](https://st.yandex-team.ru/NOCRFCS-6055)

## Сборка
Для обновления необходимо собрать пакет из портов.

[Общая инструкция по портам серверов Racktables.](https://wiki.yandex-team.ru/noc/racktables/noc-myt/sas-ports/)
1. Клонировать репозиторий:  
```
git clone ssh://git@bb.yandex-team.ru/noc/freebsd-8-ports.git
git checkout noc12n
```
2. Изменить _ARC_TAGNAME_ на актуальный svn_revision из [Arcadia](https://a.yandex-team.ru/arc/history/trunk/arcadia/noc/alexandria).   
```
freebsd-8-ports/browse/alexandria/Makefile
```
3. Применить изменения и обновить репозиторий (`git add, git commit, git push origin noc12n`).
4. Подтянуть изменения и пересобрать пакет  
```
sudo poudriere ports -p noc12rt-local -u
sudo poudriere bulk -j noc12rt -p noc12rt local/alexandria
```
5. Готовый пакет  
```
/poudriere/data/packages/noc12rt-noc12rt/All/Alexandria-1.0.0_{snv_revision}.txz
```

## Установка
#### Копирование и установка архива:  
```
scp noc-cfe2.yndx.net:/poudriere/data/packages/noc12rt-noc12rt/All/alexandria-1.0.0_{snv_revision}.txz ~
sudo pkg install alexandria-1.0.0_8478533.txz
```
#### Перезапуск сервиса:  
```
sudo service alexandria stop
sudo service alexandria start
sudo service alexandria status
```
#### Проверка Syslog: 
`/var/log/alexandria.log`


## Изменение настроек
### Настройки Alexandria:  
`/usr/local/etc/alexandria.yaml`

{% note info %}

Для применения настроек может понадобиться "sudo service nginx reload"

{% endnote %}

### Настройки php-fpm Racktables:  
```
git@noc-gitlab.yandex-team.ru:nocdev/configs.git
/usr/local/configs/php-fpm/rt.conf
```

{% note info %}

Адрес сервера Alexandria для sw-ver-report определяется переменной "env[ALEXANDRIA_URL]", по умолчанию localhost.

{% endnote %}