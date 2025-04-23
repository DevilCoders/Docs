# Обновление паролей SSID на точках доступа и контроллерах

## Что это
Короче, на standalone wi-fi точках доступа и на беспроводных контроллерах нужно обновлять пароли на некоторых SSID. Для этого в RT есть машинерия запускаемая по крону для периодического выполнения этих операций.

## Управление поведением
### Теги
Следующие теги вешаются, когда хочется чтобы RT попробовал обновить пароли для этого SSID на девайсе:
- `{запароленный ssid Guests}`
- `{ssid MobCert}`
- `{ssid MobTest}`
- `{ssid MobTestContractors}`
- `{ssid MobDevInternet}`
- `{ssid MobDevInternet}`
- `{ssid MobDevHotSpot}'`

### Cron
Подробнее тут: `scripts/update-rt-crontab.sh`
Запускается обновление сейчас так:
- `MobCert` каждый день в 04:03
- `Guests` каждую неделю в Воскресенье в 01:06
- `MobTest` первое Воскресенье месяца в 01:09
- `MobDevInternet` первое Воскресенье месяца в 01:12
- `MobDevHotSpot` первое Воскресенье месяца в 01:18
- `MobTestContractors` первое Воскресенье месяца в 01:24

Скрипт принимает аргументы. Чтобы в режиме диалога передать пароль, а не генерировать новый, то необходимо указать аргумент "-".
```bash
usage: racktables-set-wifi-password.php (Guests|MobCert|MobTest|MobDevInternet) [ - ]

if second arg is -, the password is read from STDIN
```

### Логирование
Логи, где и как обновилось записывается на страницы Wiki, которые будут описаны ниже (сорян)

## Куда смотреть
Смотреть нужно в основном в `scripts/racktables-set-wifi-passwords.php`, разное используемое там раскидано по другим частям в РТ.

На вход получает на каком SSID хотим обновить пароли. Дальше по различным предикатам ищем, где этот SSID присутствует.

После определяем `breed` по `mgmt_type` для каждого из найденных девайсов (часть `breed` заведена в `racktables-upstream`, часть добавлена в `plugins/local.php`)

__Поддерживаются:__ Cisco Standalone AP, Cisco WLC, Aruba IAP, Aruba WLC

Явки и пароли для точек и контроллеров Aruba получаются через `terminal_settings` в `secret_common.php`, а хранятся на `noc-sas` и `noc-myt` в `/home/racktables/yandex_secrets.php`

Результаты обновления размещаются на wiki (со ссылкой на QR-код на disk.yandex) и отправляются в Bot:
- https://wiki.yandex-team.ru/diy/wifi/guestpass/
- https://wiki.yandex-team.ru/diy/wifi/mobcertpass/
- https://wiki.yandex-team.ru/diy/wifi/mobtestpass/
- https://wiki.yandex-team.ru/diy/wifi/MobTestContractors/
- https://wiki.yandex-team.ru/diy/wifi/MobDevInternet/
- https://wiki.yandex-team.ru/diy/wifi/MobDevHotSpot/


