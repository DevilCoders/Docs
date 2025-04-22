# tsum-helper-chrome-extention

[Страница с описанием проекта](https://wiki.yandex-team.ru/users/atztec/chrome/ybrouser-plagin-dlja-uproshhenija-zhizni-pri-rabote-s-cum/)
## Prerequisites

* [node + npm](https://nodejs.org/) (Current Version)

## Option

* [Visual Studio Code](https://code.visualstudio.com/)

## Includes the following

* TypeScript
* Webpack
* React
* Jest
* Example Code
    * Chrome Storage
    * Options Version 2
    * content script
    * count up badge number
    * background

## Project Structure

* src/typescript: TypeScript source files
* src/assets: static files
* dist: Chrome Extension directory
* dist/js: Generated JavaScript files


## 1. Как установить в chrome/y-browser

для установки:
  - скачать по ссылке [тык](https://pages.github.yandex-team.ru/market/tsum-helper-chrome-extention/gh-pages/dist_latest.crx)
  - перейти в вкладку расширений, для y-browser ввсести в адрес `browser://extensions/`
  -  перейти в режим разработки, переключатель находится справа вверху ![скрин](https://jing.yandex-team.ru/files/atztec/screenshot-nimbus-capture-2021.11.02-23_14_25.png)
  -  перетащить скачанный файл на вкладку с `browser://extensions/` согласиться с установкой
  -  при возникновении ошибок перезапускать расширение из вкладки `browser://extensions/` 
  ![скрин](https://jing.yandex-team.ru/files/atztec/screenshot-nimbus-capture-2021.11.02-23_17_28.png)


## 2. Setup for develop

```
npm install
```

## 3. Собрать для использования или запаковки в пакет

```
npm run build
```

## 4. Собрать для разработки в watch режиме

### terminal

```
npm run watch
```

## 5. Test
`npx jest` or `npm run test`
