# @yandex-int/captcha [WIP]

Общий компонент капчи.

<p align="center">
  <img src="https://jing.yandex-team.ru/files/yarastqt/preview.png" />
</P>

## 🔗 Содержимое

* [Установка](#установка)
* [Начало работы](#начало-работы)
* [Использование](#использование)
* [Разработка](./contribute.md)

## 📦 Установка

**peer-зависимости:**

```sh
npm i -PE @yandex-int/i18n @bem-react/core @bem-react/classname @bem-react/di --registry http://npm.yandex-team.ru
```

**основной пакет:**

```sh
npm i -PE @yandex-int/captcha --registry http://npm.yandex-team.ru
```

## ✨ Использование

Компонент доступен на двух платформах:

* **desktop** — `@yandex-int/captcha/Captcha/desktop`
* **touch-phone** — `@yandex-int/captcha/Captcha/touch-phone`

**Базовый сценарий:**

```ts
import { Captcha } from '@yandex-int/captcha/Captcha/desktop'

const Form = () => {
  return (
    <Captcha />
  )
}
```

**Продвинутый сценарий:**

Если по каким-то причинам `desktop` или `touch-phone` не подходят, то можно собрать свой вариант капчи у себя на проекте. `@yandex-int/captcha` экспортирует компоненты `CheckboxCaptcha`, `AdvancedCaptcha` и хук `useCaptchaState`, из которых можно собрать необходимый вам вид капчи.

```ts
import React, { FC, useRef } from 'react';
import { useCaptchaState, CheckboxCaptcha, AdvancedCaptcha } from '@yandex-int/captcha'
import { Popup, ThemeProvider } from '@yandex-int/captcha/lib/lego';
import { CaptchaProps } from '@yandex-int/captcha/Captcha/types';
export const Captcha: FC<CaptchaProps> = (props) => {
  const anchorRef = useRef<HTMLDivElement>(null);
  const scopeRef = useRef<HTMLDivElement>(null);
  const { captchaProps, popoverProps } = useCaptchaState(props);
  return (
    <ThemeProvider>
      <div ref={scopeRef} className="Captcha">
        <CheckboxCaptcha {...captchaProps} anchorRef={anchorRef} />
        <Popup {...popoverProps} anchor={anchorRef} scope={scopeRef}>
          <div className="Captcha-PopupContent">
            <AdvancedCaptcha {...captchaProps} />
          </div>
        </Popup>
      </div>
    </ThemeProvider>
  );
};
```

**Язык капчи:**

Капча берет язык из контекста `@yandex-int/i18n/lib/react`

Пример изменения языка:

```ts
import { Lang } from '@yandex-int/i18n/lib/react';
import { Captcha } from '@yandex-int/captcha/Captcha/desktop'

const Wrapper = () => {
  return (
    <Lang.Provider value={{lang: 'en' }}>
      <Captcha />
    </Lang>
  );
}
```

Важно! чтобы инстансы `@yandex-int/i18n` были одинаковы на проекте и в капче. Для этого в webpack нужно добавить алиас на пакет:

```ts
const webpackConfig = {
  ...restFields,
  resolve {
    extensions: ['.tsx', '.ts', '.js'],
    symlinks: true,
    alias: {
      '@yandex-int/i18n': path.resolve('node_modules/@yandex-int/i18n'),
    },
  }
}
```

**Подписка на валидацию:**

```ts
import { Captcha } from '@yandex-int/captcha/Captcha/desktop'

const Form = () => {
  const onValidate = (token?: string) => {
    // do stuff
  }

  return (
    <Captcha onValidate={onValidate} />
  )
}
```
