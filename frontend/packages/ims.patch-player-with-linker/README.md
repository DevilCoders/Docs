# ims.patch-player-with-linker

Пакет позволяет заинжектить ответ [линкера](https://clubs.at.yandex-team.ru/vp/126)
в конфигурацию [плеера](https://github.yandex-team.ru/IMS/video-player-iframe-api) или песочницы.

## Немного об ожидаемых параметрах
Обе функции из пакета ожидают на вход **опциональные** аргументы:
- slots - string - слоты в формате "123,0,1;321,0,10", которые уже существуют у сервиса. Если слотов нет - можно использовать генерацию их из тестидов вида: `slots = testids.map(testid => testid+',0,-1').join(';')`
- linker - object - тело ответа из линкера. О том как его подключить лучше уточнять у текущего [дежурного команды web-плеера](https://abc.yandex-team.ru/services/video-player/duty/?role=1388)

## patchPlayerConfig
Функция для инжекта внутрь конфигурации PlayerApi.
На вход принимает config (оригинальная конфигурация), slots, linker.
Возвращает **мутированный** объект config.
Нужно использовать для вставок через `Ya.playerApi.init`. Пример:
```typescript
import { patchPlayerConfig } from '@yandex-int/ims.patch-player-with-linker'

const slots: string | undefined | null = "123,0,1";
const linker: unknown = { /* тут будет содержимое ответа линкера */ };

const config = { /* оригинальный конфиг, который собрал сервис */ };

Ya.playerApi.init(patchPlayerConfig({ config, linker, slots }));
```

## patchQuery
Функция для инжекта внутрь query Ya.VH.PlayerJS#update().
На вход принимает query (оригинальная query), slots, linker.
Возвращает **мутированный** объект query.
Нужно использовать для вставок, использующий Sandbox. Пример:
```typescript
import { patchQuery } from '@yandex-int/ims.patch-player-with-linker'

var player = new Ya.VH.PlayerJS('#container1');

const slots: string | undefined | null = "123,0,1";
const linker: unknown = { /* тут будет содержимое ответа линкера */ };
const config: string | object = { /* какая-то конфигурация плеера песочницы */ };
const query = { /* оригинальный query, который собрал сервис */ };

player.update(config, patchQuery({ query, linker, slots }));
```

## Установка
```
npm i @yandex-int/ims.patch-player-with-linker
```
