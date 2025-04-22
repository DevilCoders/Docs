# Пакет для компонентов единого публичного профиля (ЕПП)

## Установка

`npm i -S @yandex-int/epp`

## Использование

```ts
import { EppHeader } from '@yandex-int/epp/EppHeader';
```

```ts
// TabKey: 'collections' | 'znatoki' | 'ugc' | 'district'
<EppHeader
    activeTab="ugc"
    serviceUsage={backendData.serviceUsage} // Record<TabKey, boolean>
    background="#394156"
    color="#fff"
    publicUserId={'public id'}
    tld={'ru'}
/>
```
По-умолчанию активный сервис становится на первое место. Чтобы порядок сервисов сохранялся, нужно передать пропсу `fixedOrder`.
По-умолчанию цвет икоки соответствует свойству color. Чтобы цвет икоки отличался от цвета текста, следует использовать пропсу `iconColor`.

## Разработка

1. `npm i`.
2. `npm start`.
3. Открыть в браузере `public/index.html`.
4. При изменении исходного код в папке `src` webpack пересоберёт бандл и изменения можно будет увидеть, обновив страницу.

Подключить изменённый пакет к сервису:
1. Выполнить `npm link` в директории пакета.
2. Выполнить `npm link @yandex-int/epp` в директории сервиса.
3. Собрать актуальную версию пакета `npm run build` в директории пакета.
