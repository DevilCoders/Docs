# Грибные карточки

Обобщенный колдунщик для многих сервисов, в основе которых карусель с карточками или 1-2 карточки из лучших ответов.

## Исходные требования
- простая и обощенная декларация данных (plain object)
- конфигурируемый / параметризуемый набор элементов под каждый сервис (ordering & visual options)
- возможность проведения экспериментов с порядком и содержимым карточек (over backend & expFlags)
- максимальное переиспользование готовых блоков конструктора
- максимальная опциональность
    - нет данных = нет элемента,
    - нет декларации элемента = либо деградируем до известного / либо не рендерим элемент,
    - нет конфига = деградируем до дефолтного конфига.

## Данные и эксперименты
### Данные
Бэкенд собирает данные от разных источников и приводит их к одному плоскому виду, где не должны быть пустых полей. Данные приходят в поле `construct.*.data`. Данные поставляются в произвольном варианте.

```typescript
interface IMushroomSnippet {
    title: string;
    url: string;
    text: string;
    path: Array<{
    	url: string;
    	text: string;
    }>;
    data: Array<IMushroomData>;
    config?: IMushroomConfig;
}

interface IMushroomData {
    url?: string;
}
```
![Маппинг полей](https://jing.yandex-team.ru/files/meison/browser_VJ04uQarIn.png)

### Конфиг

Структура конфига `construct.*.data` представляет собой объект со следующей структурой:

```typescript
export interface IMushroomConfig {
    cardWidth?: number;
    firstCardWidth?: number;
    singleCardFullwidth? : boolean;
    keyset?: KeysetDictionary; // { ru: {key: 'translate'}, en: }
    order?: Array<IMushroomSlot>;
    more?: {
        count: number;
        url?: string;
        i18nKey: string;
    };
    ariaBindings?: Array<{ value?: string; path?: string}>;
}
```



`cardWidth` — ширина карточек в количестве колонок 12-тиколоночной сетки.

`firstCardWidth`  — ширина первой карточки в колонках 12-тиколоночной сетки

`keyset` — дополнительные ключи для переводов. Необходимы для быстрых экспериментов, когда необходимых переводов нет на верстке.

**Пример:**

Обычная форма:

```js
"ru": {
    "Ещё вопросы?": "Ещё вопросы?"
}
```



**Плюрализованная форма:**

```js
"ru": {
    "{count} нравится": {
        "one": "{count} падабаецца",
        "some": "{count} падабаецца",
        "many": "{count} падабаецца",
        "none": "Падабаецца"
      }
}
```



⚠ для динамических ключей поддерживается только одно поле `count`



`singleCardFullwidth` — флаг для варианта с одной карточкой.

`more` — объект описывающий плашку "Ещё" для карусели карточек.

```js
{
    count: number; // общее количество элементов включая те, которые уже были показаны
    url?: string; // ссылка на кнопке
    i18nKey: string; // ключ переводов, на кнопке Ещё
}
```



`ariaBindings` — данные для формирования `ariaLabel` для ссылки карточки. Позволяет указать или ключ перевода\фиксированный текст ( поле `value` ) или [lodash-путь](https://lodash.com/docs/4.17.15#property) внутри объекта с данными карточки. Передавается как массив, результаты скдеиваются через пробел.

**Формат:**

`Array<{ value?: string; path?: string}>;`



`order` — порядок отображения и правила получения данных для примитивных блоков карточки. Представляет собой массив конфигов для каждого [примитивного блока](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/). Порядок расположения в массиве определяет порядок отображения.

**Конфиг отображения [примитивного блока](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/):**

```typescript
interface IMushroomSlot {
    type: EMushroomSlotType;
    bindings?: Record<string, string>;
    i18nKeys?: Record<string, string>;
    defaultProps?: Record<string, TMushroomProp>;
    gap?: 'm' | 'l';
    items?: Array<IMushroomSlot>;
}
```



`type` — тип примитивного блока

`bindings` — объект сопоставления свойств примитивного блока и значения в данных  карточки

**Формат:**

```js
{
	"<ключ свойства примитивного блока>": "<lodash-путь до значения в объекте карточки>"
}
```

`defaultProps` — объект со значениями по умолчанию для примитивного блока

**Формат:**

```js
{
	"<ключ свойства примитивного блока>": "<значение по умолчанию>"
}
```

`i18nKeys` —  объект сопоставления свойств примитивного блока и ключ переводов

**Формат:**

```js
{
	"<ключ свойства примитивного блока>": "<ключ перевода>"
}
```

`gap` — отступ справа от примитивного блока. Применимо только блока типа `meta`.

`items` — массив вложенных примитивных блоков. Применимо для блоков-контейнеров.



#### Примитивные блоки

##### text: Текст

Блок [mushroom-text](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-text)

[Свойства и пример использования](https://serpdocs.si.yandex-team.ru/constructives/mushroom-text)

[Внешний вид](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/#link-tekst)

##### textWithIcon: текст с иконкой

Блок [mushroom-text-with-icon](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-text-with-icon)

##### divider: разделитель между блоками

Блок [mushroom-divider](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-divider)

[Внешний вид](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/#link-razdelitel)

##### container: вертикальный контейнер

Блок [container](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/container)

содержит в себе только поле `items`, которое содержит массив примитивных блоков

##### meta: горизонтальный контейнер

Блок [mushroom-meta](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-meta)

[Внешний вид](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/#link-meta)

##### user: иконки и описание пользователя

Блок [mushroom-user](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-user)

[Свойства и пример использования](https://serpdocs.si.yandex-team.ru/constructives/mushroom-user)

[Внешний вид](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/#link-polzovatel)

##### date: дата

Блок [mushroom-date](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-date)

[Свойства и пример использования](https://serpdocs.si.yandex-team.ru/constructives/mushroom-date)

##### cover: картинка с лейблами

Блок [mushroom-cover](https://serpdocs.si.yandex-team.ru/constructives/mushroom-cover)

[Свойства](https://serpdocs.si.yandex-team.ru/constructives/mushroom-cover)

[Внешний вид](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/#link-kartinka)

##### social-reactions:  блок лайков\дизлайков

⚠ Необходимо реализовать обработку отработку доставки\получения информации о поставленном лайке\дизлейке самостоятельно ([пример](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/social-reactions/_q/social-reactions_q.js))

Блок [social-reactions](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/social-reactions)

[Свойства](https://serpdocs.si.yandex-team.ru/constructives/social-reactions)

[Внешний вид](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/#link-deistviya)

##### footer: подвал карточки

Блок [mushroom-footer](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/mushroom-footer)

##### video: видео карточка

Блок [video2](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/video2)

[Свойства и пример использования](https://serpdocs.si.yandex-team.ru/constructives/video2)


### Заведение конфига
- Продовый конфиг типовой карточки (q, zen, etc) хранится на фронте в Mushroom.const.ts и работает всегда.
- Экспериментальный конфиг типовой карточки приходит из данных в поле `construct.*.config` и применяется только при наличии 2 флагов:
- `beauty_mushroom_{q|zen}_enabled={0|1}` – системный флаг верскти, разрешающий брать конфиг из данных
- `beauty_mushroom_{q|zen}_config={string name}` – системный флаг бекенда, включающий именованый конфиг в доставку с данными
- экспериментальные конфиги должны храниться в Аркадии, их пишут фронтендеры под эксперименты продакта, пушат в аркадию через arc / svn, вливаются в транк.
- собираться в виде данный для fastres-rearr пакета с регулярностью 1 раз в час и релизятся в прод.
- имя конфига соответствует имени файла в аркадии, должно выглядеть так `beauty_mushroom_zen_big-title`, где:
  - `beauty`- название v-team
  - `mushroom` – тип адаптера
  - `zen` – подтип адаптера
  - `big-title` – понятное человекочитаемое название экспериментального конфига

## Счетчики
```TODO```



## Дизайнеру

Описание карточек можно посомтреть [здесь](https://depot.yandex-team.ru/guidelines/bloki/cards-constructor/)

