### Troubleshooting
Список юнитов запущеных на хосте можно получить
`/opt/hostctl/bin/hostctl list`

Посмотреть статусы юнита `/opt/hostctl/bin/hostctl status <unit-name>`
* Ready
  > Ревизия применилась без ошибок
* Changed
  > Юнит получил изменения при последнем запуске hostctl
* Throttled
  > Юнит потротлился об Orly
* Removed
  > Юнит был успешно удален
* Conflicted
  > У юнита есть конфликты с другими юнитами

Посмотреть spec/meta/status/revs юнита `/opt/hostctl/bin/hostctl show <unit-name>`

Также полезно посмотреть в лог `tail -100 /var/log/hostctl.log`.
