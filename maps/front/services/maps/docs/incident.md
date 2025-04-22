# Что делать в случае факапа?

- [Откат релиза](#rollback)
- [Отключение бекенда](#backend)
- [Снятие трафика с одного из ДЦ](#its)
- [RPS Limiter](#rps-limiter)
- [DDoS](#ddos)

## Откат релиза {#rollback}

Если понимаем, что проблема в релизе, то делаем следующее:

1. Перейти во вкладку [History](https://deploy.yandex-team.ru/stage/maps-front-maps_production/history).
2. Выбрать предыдущий релиз по номеру тега.
3. Нажать **Apply** > **Apply as is**.
4. В открывшемся сравнении нажать **Deploy**.

## Отключение бекенда {#backend}

При острой необходимости есть возможно отключить походы в конкретные бекенды. Для этого необходимо:

1. Выяснить ключ в терминах [host_config/inthosts](../../../tools/hosts/).
2. Добавить его в поле `server.disabledIntHosts` в [основной конфиг](https://bunker.yandex-team.ru/maps-www/production/config?view=raw) бункера.
3. Нажать "Сохранить и опубликовать".

После этого в течение минуты конфиг применится на всех инстансах приложения.

<details><summary>Пример конфига</summary>

```json
{
    "server": {
        "disabledIntHosts": {
            "router": true
        }
    }
}
```

</details>

## Снятие трафика с одного из ДЦ {#its}

**Важно**: помните, что это управление весов только инстансов. Трафик внутри балансера всё равно будет приходить во все ДЦ.

Можно управлять весами распределения трафика через [ITS](https://wiki.yandex-team.ru/runtime-cloud/nanny/its/):

-   [front-maps.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/l7heavy/front-maps.slb.maps.yandex.net/)

> Кроме того, можно слить часть трафика через `DEVNULL`.

После изменений нажать "_Save sections weight_" и затем "_Push to ITS_".

## Выполнить произвольную команду на всех инстансах

**Важно**: нужно, чтобы стоял [qeq](https://a.yandex-team.ru/arc_vcs/maps/front/packages/qeq).

Шорткаты для выбора инстансов:

| Сервис | Селектор |
|---|---|
| БЯК | `yd:maps-front-maps_production.maps.maps_box` |
| Метро | `yd:maps-front-maps_production.metro.metro_box` |
| Виджет | `yd:maps-front-maps_production.map-widget.map-widget_box` |

Само выполнение команды происходит в конкретном ДЦ:

```bash
qeq exec $(SELECTOR)@man -- supervisorctl status
```

## RPS Limiter {#rps-limiter}

Часть запросов можно ограничить через нашу секцию в [RPS Limiter](https://rpslimiter.z.yandex-team.ru/records/maps_front/front-maps/editor).

Детальнее про настройку конфигурации читайте в [документации сервиса](https://wiki.yandex-team.ru/rpslimiter/users/#konfigurirovanie).

## DDoS {#ddos}

**Важно**: _не уверен — не кати_.

В случае серьезного DDoS можно заблокировать запросы по IP или регулярке, для этого есть сервис "[Единая база блокировок](https://wiki.yandex-team.ru/jandekspoisk/sepe/antirobotonline/servicecbb/)".

Наши группы расположены под тегом [#cbbmaps](https://cbb-ext.yandex-team.ru/tag/cbbmaps):
- [maps_captcha_ip](https://cbb-ext.yandex-team.ru/groups/846)
- [maps_captcha_re](https://cbb-ext.yandex-team.ru/groups/847)
- [maps_403_ip](https://cbb-ext.yandex-team.ru/groups/848)
- [maps_403_re](https://cbb-ext.yandex-team.ru/groups/849)
- [maps_mark_re](https://cbb-ext.yandex-team.ru/groups/850)

Группы по IP (`maps_captcha_ip` и `maps_403_ip`) используем в редких случаях для точечных блокировок. При этом проверить такие блокировки до продакшена не получится.

Для блокировки по регулярке действуем по следующей схеме:
1. Собираем регулярку через `maps_mark_re`, они будут только "размечать" запросы, но не блокировать. Синтаксис регулярок можно найти [на вики ЕББ](https://wiki.yandex-team.ru/jandekspoisk/sepe/antirobotonline/docs/antiddos-tool/).
1. Смотрим на [график "Разметка"](https://yasm.yandex-team.ru/template/panel/antirobot_for_service/service=maps/). Запросов от залогинов или доверенных **не должно быть**.
1. Переносим в `maps_captcha_re` или `maps_403_re`.

Если что-то не понятно или не хватает прав, то сразу идем в [чат поддержки](https://t.me/joinchat/AAYTqU_d3lVprRylyw_z5g).
