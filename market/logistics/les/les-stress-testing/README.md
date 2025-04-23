# Пакет для стресс тестирования LES
## Про конфижики
Чтобы обновить патроны, нужно загрузить их в сендбокс командой `ya upload --do-not-remove sqs_events_add_ammo.yml` и после того, как команда выдаст что-то подобное
```
Created resource id is 2597172708
	TTL          : 14 days
	Resource link: https://sandbox.yandex-team.ru/resource/2597172708/view
	Download link: https://proxy.sandbox.yandex-team.ru/2597172708
```
взять resource id `2597172708` и прописать его в ссылке конфига, примерно так `ammofile: 'https://proxy.sandbox.yandex-team.ru/2597172708'`
А дальше, коммитим файлик конфига, мержим его в транк и готово, можно стрелять

## Ссылочки
- Тут конфиги для танков (сделано по [доке](https://wiki.yandex-team.ru/Load/howto/simple-start/#podgotovkaokruzhenija)) 
- Тут патроны для танков (сделано по [доке](https://wiki.yandex-team.ru/load/guides/ammo))
- На будущее, для мониторингов [дока](https://wiki.yandex-team.ru/load/guides/solomon-plugin/)
- Тикет в лунапарке [тыц](https://lunapark.yandex-team.ru/DELIVERY-32738)
