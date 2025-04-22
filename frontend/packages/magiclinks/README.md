# @yandex-int/magiclinks

Библиотека для раскрытия в браузере гиперссылок (`<a href>`) в «Магические ссылки».

Работает на любом `html`, можно использовать вместе с `React`.

## Как работает
Библиотека запускает `MutationObserver` на `DOM` узлах,
которые будут ей указаны и следит за элементами `a[href]`.
Найденные узлы раскрываются в магические ссылки.

## Использование
```js
// 1. Проимпортировать библиотеку в браузерном коде
import { MagicLinks } from '@yandex-int/magiclinks';

// 2. Проинстанцировать класс
const magicLinks = new MagicLinks()
    // 3. Добавить элемент, внутри которого будут работать магические ссылки
    .addConsumption(document.querySelector('#MyMagiclinksRoot1'))
    // Можно добавить сколько угодно таких элементов
    .addConsumption(document.querySelector('#MyMagiclinksRoot2'))
    .addConsumption(document.querySelector('#MyMagiclinksRoot3'), {
        // Можно добавиль фильтрацию, чтобы не трогать некоторые гиперссылки
        filter(url, href, ctxElem) {
            return url === href.innerText;
        },
    });

// Аналог деструктора - просто удалить все контексты:
magicLinks
    .delConsumption(document.querySelector('#MyMagiclinksRoot1'))
    .delConsumption(document.querySelector('#MyMagiclinksRoot2'))
    .delConsumption(document.querySelector('#MyMagiclinksRoot3'));
```

## Сборка
**Рекомендуемый способ использования** библиотеки – *скомпилировать* ее в бандле своего приложения.

Но, в случае если у вас нет доступа к коду сервиса, или у вас нет `webpack`, то можно воспользоваться командой

```bash
npm run bundle
```

Команда соберет артефакты библиотеки в виде 2х файлов:

```bash
build/bundle.css
build/bundle.js
```

Эти файлы можно подключить к проекту любым доступным вам способом и использовать глобальную переменную `window.MagicLinks`
