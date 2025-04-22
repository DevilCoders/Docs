# @ps-int/ps-tanker

Пакет для работы с локализацией в Персональных Сервисах (ПС).

## Содержание
- [Быстрый старт](#Быстрый-старт)
- [Работа с локалями](#Работа-с-локалями)
  - [Оптимальная конфигурация webpack](#Оптимальная-конфигурация-webpack)
  - [Использование собранных артефактов](#Использование=-собранных-артефактов)
- [Конфигурация](#Конфигурация)  
  - [Общие параметры](#Общие-параметры)
  - [Параметры загрузки локалей](#Параметры-загрузки-локалей)
  - [Параметры webpack сборки](#Параметры-webpack-сборки)
  
## Быстрый старт
```shell script
# main dependency
npm i @ps-int/ps-tanker

# peer/optional dependencies
npm i react webpack

# start interactive initialization
npx ps-tanker
```
Запустится интерактивный режим настройки проекта.

Если в вашем проекте еще нет файла конфигурации для танкера, вам предложат создать его.

Иначе будут доступны опции по донастройке конфигурации и скачиванию последней версии локалей. 

## Работа с локалями
Когда локали загружены, с ними можно работать как с обычными TS модулями.
```javascript
import { someKey, someParamKey } from './locales/i18n/some-project/some-keyset/some-key';

console.log('Обычный ключ', someKey);
console.log('Ключ с параметрами', someParamKey({
    someParam: 'someString'
}));
```

Каждый ключ является отдельным модулем.
Внутри для подгрузки языков используется `require.context`. 

Страница узнает о текущем языке из переменной `process.env.PSTANKER_LANGPARAM`, которая по умолчанию резолвится в `window.lang`.

### Оптимальная конфигурация webpack
К проекту добавлена оптимальная конфигурация webpack, для работы с локалями.
Это не плагин, а обертка над всем конфигом.

#### Пример использования:
```javascript
// webpack.config.js

const withLocales = require('@ps-int/ps-tanker/webpack');

module.exports = withLocales({
   ...
});
```

#### Производятся следующие модификации:

<details>
<summary>- выносим локали в отдельные чанки по имени кейсета</summary>

```javascript
{
    optimization: {
        splitChunks: {
            cacheGroups: {
                i18n: {
                    test: <locales dir matcher>,
                    name: <locales chunks name>,
                    chunks: 'all',
                    enforce: true,
                }           
            }
        }       
    }
}
```

</details>

<details>
<summary>- оптимизируем код генерируемый `require.context` для локалей</summary>

```javascript
{
    plugins: [
        new CompactContextPlugin(options)
    ]
}
```  

</details>
    
<details>
<summary>- не собираем ключи, которые импортируются в коде, но не используются</summary>

```javascript
{
    optimization: {
        usedExports: true 
    },
    plugins: [
        new NoSideEffectsPlugin(options)
    ]
}
```

</details>
    
<details>
<summary>- генерируем блок html шаблона для оптимальной загрузки языков на клиенте </summary>

- [описание плагина](./webpack/plugins/HtmlTemplateExtras)
```javascript
{
    plugins: [
        new HtmlTemplateExtrasPlugin(options)
    ]
}
```

</details>

<details>
<summary>- модифицируем рантайм для оптимальной загрузки языков на клиенте</summary>

- [описание плагина](./webpack/plugins/ModuleTemplateExtras)
```javascript
{
    plugins: [
        new ModuleTemplateExtras(options)
    ]
}
```

</details>

<details>
<summary>- расширяем ps-build манифест информацией про языковые бандлы</summary>

- [ps-build манифест](../ps-build/lib/webpack/plugins/ServerManifestPlugin)
- [описание плагина](./webpack/plugins/ServerManifestExtras)

```javascript
{
    plugins: [
        new ServerManifestExtrasPlugin(options)
    ]
}
```

</details>
  
<details>
<summary>- настраиваем переменную из которой берется язык</summary>

```javascript
{
    plugins: [
        new webpack.DefinePlugin({
            'process.env.PSTANKER_LANGPARAM': options.langParam
        })
    ]
}
```

</details>  

## Конфигурация

### Общие параметры
#### language
**Обязательный параметр**

Единственный источник правды о поддерживаемых проектом языках.

**Тип**: string[]<br>
**Пример**: `[ "ru", "en" ]`<br>

### Параметры загрузки локалей
#### project-id
**Обязательный параметр**

Идентификатор проекта в Танкере, откуда нужно выкачать локали.

**Тип**: string<br>
**Пример**: `mail-liza`<br>

#### outputDir
**Обязательный параметр**

Локальная директория относительно .tanker.json в которую нужно выкачать локали.

**Тип**: string<br>
**Пример**: `./locales`<br>

#### keyset-id
Идентификаторы кейсетов в проекте в Танкере, которые нужно выкачать.
Может быть пустым, тогда будут выкачаны все кейсеты.

**Тип**: string[]<br>
**Пример**: `[ "testing-keyset-1", "testing-keyset-2" ]`<br>

#### safe
Язык перевода, который подставляется вместо незаполненных переводов.

**Тип**: string<br>
**Пример**: `"en"`<br>
**Дефолт**: `"ru"`<br>

#### jsx
Включает обработку html разметки при генерации переводов.

**Тип**: boolean<br>
**Пример**: `false`<br>
**Дефолт**: `true`<br>

#### strings
Включает режим упрощения ключей. Если в ключе нет параметров, он превращается в строку.
Позволяет экономить место в финальном бандле с языком.

**Тип**: boolean<br>
**Пример**: `false`<br>
**Дефолт**: `true`<br>

### Параметры webpack сборки
#### langParam
**Обязательный параметр**

Рантайм плейсхолдер текущего языка.

**Тип**: string<br>
**Пример**: `'__webpack_require__.lang'`<br>
**Дефолт**: `'window.lang'`<br>

#### modifyRuntime
Включает модификацию webpack рантайма. ([подробнее](./webpack/plugins/ModuleTemplateExtras))

**Тип**: boolean<br>
**Дефолт**: `false`<br>

#### modifyManifest
Включает модификацию серверного манифеста в ps-build сборке. ([подробнее](./webpack/plugins/ServerManifestExtras))

**Тип**: boolean<br>
**Дефолт**: `false`<br>

#### modifyTemplate
Включает модификацию html шаблона. ([подробнее](./webpack/plugins/HtmlTemplateExtras))

**Тип**: boolean | [object](./webpack/plugins/HtmlTemplateExtras/README.md#modifytemplate)<br>
**Дефолт**: `false`<br>

#### extractChunks
#### optimizeExports
#### optimizeContexts
