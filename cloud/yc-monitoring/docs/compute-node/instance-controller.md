[Алерт в Juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Dinstance-controller)

## instance-controller

Сигнализирует о проблемах в instance controller'е (per-instance среда исполнения тасок и синхронизации стейта с Compute).

## Подробности

Скорее всего, никогда не загорится, т. к. на данный момент сделан на всякий случай, чтобы мониторить corner cases, которые скорее всего никогда не произойдут:
* Количество событий в очереди target state таски. Сработает, если таска по какой-то причине залипнет на долгое время, но кто-то будет генерить новые события.
* Количество Compute'ных тасок в local state (гипотетически могут начать копиться, если Compute API перестанет их принимать, либо если Compute API будет очень долгое время недоступно, а инстанс будет постоянно крешиться и генерить этими крешами эвенты для Compute API).
* Количество Compute'ных событий в Compute'ных тасках.

## Диагностика

В деталях проверки будет список инстансов вместе с описанием проблемы.
