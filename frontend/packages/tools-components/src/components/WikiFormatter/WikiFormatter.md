# WikiFormatter

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/WikiFormatter'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

Компонент, предназначенный для форматирования вики-разметки

## Пример подключения

```jsx
import { WikiFormatterDesktop } from '@yandex-int/tools-components/WikiFormatter/desktop';

// ***

<WikiFormatterDesktop nonce="<nonce>">
  **Привет**
</WikiFormatterDesktop>
```

## Свойства
Единственным обязательным свойством является [`nonce`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/nonce).

WikiFormatter-у необходимо встроить некоторый inline-js, который он получит из wfaas.yandex-team.ru, поэтому необходимо такое разрешение.

Wiki-разметка передается через `children`. Особенность: `children` — это строка, которая может содержать неэкранированную html-разметку. WikiFormatter прогонит её через санитайзер и преобразует в безопасный HTML. Теги, которые санитайзер посчитает безопасными, останутся (например, `<b></b>`). Однако всё, что ему покажется опасным, пропадёт из результата.

Также есть свойство `settings` - настройки форматтера, подробнее о нем можно прочитать [здесь](https://github.yandex-team.ru/frontend/tools/blob/master/packages/woof/server.d.ts#L41)

Для того, чтобы определить момент завершения рендеринга Вики-форматера в компоненте, можно
передать необязательное свойство `onContentUpdated` – функция, которая будет вызываться после инициализации форматтера. `onContentUpdated` вызывается не единожды, а после каждого обновления контента компонента.

В основном это урлы некоторых источников данных и самого wfaas, например их может быть хотеться подменить, если нужно замокать их через clement на своем сервисе.

## Разработка

Так-как компонент посылает запросы в wfaas/schi с клиента, а на этих сервисах настроен cors, то необходимо при разработке поднять storybook под туннелером, для того чтобы все работало полноценно:

```bash
npm run build
npm start
npx tunorok --realm=yt 8100
```

На 8100 поднимается storybook

## SSR

Пока что, компонент не умеет работать прямо на сервере, но если вы самостоятельно получаете html вики-разметки c
помощью сервиса https://wfaas.yandex-team.ru, правильно отрисовать этот html на клиенте поможет компонент `<WikiFormatterHtml />`.

```jsx
import { WikiFormatterHtmlDesktop } from '@yandex-int/tools-components/WikiFormatter/desktop';

// ***

<WikiFormatterHtmlDesktop
  nonce="<nonce>"
  settings={{}}
  html={'<html...>'} // HTML, который, например, вернула ручка https://wfaas.yandex-team.ru/api/.raw_to_html
/>
```
