### Локальный запуск

1) Внести изменения в `registry`.
2) В директории `balancer/production/l7_alerts/solomon/creator/` запустить `ya make`.
3) Запустить бинарник командой `./creator`, ознакомиться с изменениями
Можно запустить команду `./creator --apply-changes` и изменения накатятся на прод.

### Секреты

Секрет, содержащий `Juggler` и `Solomon` токены:
https://yav.yandex-team.ru/secret/sec-01fzjvgwtp3b0sdb8hrpxfxvmh/explore/versions

Если возникает ошибка `'code': 'access_error'`, проверь доступ к секретам

### Документация
* Описание библиотеки Solo в [Этушке](https://lazuka23.at.yandex-team.ru/1)
* Документация по библиотеке [Solo](/arc_vcs/library/python/monitoring/solo/README.md) 
