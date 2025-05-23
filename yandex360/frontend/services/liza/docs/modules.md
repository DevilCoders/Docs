# Про модули

У нас есть следующие модули:
 1. bootstrap - загрузчик почты
 1. common - общий код для всей почты. Сюда попадает то, что не привязано к почте (lodash, es5-shim, modernizr, плагины, общий функции по работе со строкам, DOM и т.п.)
 1. nanoislads - наноострова
 2. noscript - noscript
 2. mail - общий код по работе с почтой. Сюда попадает общее для всех или нескольких страниц
  2. abook - адресная книга
  2. compose - написание письма, QR, done
  2. left - левая колонка
  3. message - просмотр письма
  4. messages - список писем
  5. setup - страницы настроек
  2. toolbar - тулбар
  6. ckeditor - отдельный модуль для ckeditor, чтобы лучше кешировался, т.к. он редко меняется
 3. promo - модуль со всеми промо + визард. Вынесен специально, он грузится и вызывается ПОСЛЕ ПЕРВОЙ ОТРИСОВКИ, чтобы никак не влиять на скорость загрузки. Этот модуль должен загружать другие нужные ему модули, иначе получится ситуация, что в mail из-за разных промо окажется половина всего кода Почты.

Код должен располагаться в нужном модуле, всеми средствами (кроме копипаста) избегайте написания кода в `mail` или `common`.
Если можно сделать дозагрузку модуля (история про модуль `promo`), лучше сделайте дозагрузку.
И не надо сразу писать код в общих модулях, потому что "это вроде бы общий код".
Располагайте код там, где он действительно используется.

## yate-модули

yate-модули импортируюся в следующем порядке

```
                nanoislands
                     |
               common+noscript
                     |
                    mail
                     |
       ______________________________________________________
       |      |       |      |        |       |      |      |
    abook  compose  left  message  messages setup  promo  toolbar
```
