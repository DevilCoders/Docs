# Yandex.Mail's new static assets

Ask kizu@ if you have any questions.

## TOC

1. [List of built static pages](#list-of-built-static-pages)
2. [Class naming notation](#class-naming-notation)
3. [Building](#building)
4. [Работа с svg-иконками](#svg)
5. [SVG-иконка с активным состоянием](#is-active)


## Class naming notation

Works like BEM, looks a bit like BEM, but not _BEM_, as we allow elements to be nested into other elements, yo.

### Structure of a name

Disclaimer: any complex names (two or more words) are written as camelCase. The first letter can be different for different entities (small for prefixes and modifiers, big for blocks and elements).

```
.mail-NestedList-Item_empty
  ↑       ↑       ↑     ↑
 (1)     (2)     (3)   (4)
```

1. Prefix. Starts with a lower latin, ends with a dash
2. Block’s name. Starts with an upper latin.
3. Element’s name. Starts with an upper latin, prefixed with a dash. Multiple nested elements allowed: `.mail-ContentToolbar-Actions-Item`
4. Modifier. Prefixed with a underscore. Both binary and complex modifiers are allowed, complex ones are used when the values are not boolean, like `_level_2` or `_3pane_vertical`.

### Prefixes

1. `mail-` — is the prefix for most blocks. We’re making “mail”, so, yeah, this.

2. `mail-ui-` — is the prefix for reusable UI blocks, like `.mail-ui-Link` or `.mail-ui-Icon`.

3. `is-` — prefix for global state modifiers like `.is-hidden`, `.is-active` etc, the name of a modifier starts with a lower latin.

4. `toggles-` — prefix for declaring the context of the toggling.

5. `toggled-by-` — prefix for declaring the subject of toggling.

### Exceptions

1. `svgicon` — is a block, telling something is a SVG icon, and could have postfix with a hub’s name, like `svgicon-boot` etc. For the time being the modifiers are written in a two dashes notation `--`, this could change on the tooling basis.



## Building

Obviously, `npm install` after cloning.

### Styles

``` sh
$ make styl
```

Compiles all the styles for everything.

### Static html

``` sh
$ make jade
```

Compiles the static pages.

### Watching

``` sh
$ make watch
```

Runs watchers for building styles and static html.

### SVG icons

``` sh
$ make svg-icons
```

### SVG icons for YATE

``` sh
$ make svg-icons-yate
```

## SVG

### Как добавить новую иконку

См. [ридми репозитория с иконками](https://github.yandex-team.ru/Daria/mail-icons#svg).

После правильного добавления иконки в репозиторий, необходимо обновить соответствующий сабмодуль — `icons` и закоммитить изменения.

### Добавление имеющейся иконки.

1. Пересобрать шаблон в динамике, в который вставляем спрайт, сейчас это index.yate. `rm neo2/src/tmpl/index/_index.*.js && make LANGS=ru`
   - Почему так? Потому что сейчас у нас галп-таск написан так, что изменения в `index.yate` не билдят выходной `_index.<lang>.js`, поэтому его нужно удалить, ну или сделать `make clean`. Это надо будет пофиксить, см. [LIZA-2019](https://st.yandex-team.ru/LIZA-2019)

2. В нужном yate-шаблоне вставить вызов функции `svg-icon('<name>')`.
   - Функция должна работать везде, если что, нужно её подключение унести повыше
   - Чтобы понять, что мы тут вообще с svg устроили, можно, например, начать с прочтения [этой статьи](http://css-tricks.com/svg-sprites-use-better-icon-fonts/) :)

### is-active

Если нужна SVG-иконка, которая переключается по изменения класса `is-active` на родителе, то в Яте она ставится вот так (на примере иконки прочитанности):

```
svg-icon('mail--Inbox-ReadSwitch', true(), 'toggled-by-active')
```

После чего на любом из родителей этой иконки, где собираемся переключать `is-active` ставим класс `toggles-svgicon-on-active`.

Всё.

Когда на блоке с `toggles-svgicon-on-active` переключается класс `is-active`, переключается и отображение иконки, больше ничего делать не нужно.

