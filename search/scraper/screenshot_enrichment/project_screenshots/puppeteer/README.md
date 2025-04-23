## fullpage/main.js

Makes screenshots and saves the html of every url in config/urls_list.txt consecutively.

Warning: uses one page instance for all screenshots, so cookies and cache may influence the content of the screenshots.

Warning: uses png to store screenshots, and as we know, png encoding is a bit slow. Switch to jpg if it suits your needs.

Warning: html is obfuscated.

Config: ```npm -i --save puppeteer```
Run: ```node fullpage.js```

## fullpage/no_images.js

Same as fullpage/main.js, but aborts request of each image request

## document/main.js

Same as fullpage/main.js, but additionally stores the screenshots of each document (element with data-cid attribute) of the page.

Включить синтаксис ES6 (лямбды и пр.) можно так https://stackoverflow.com/questions/37382108/how-to-configure-es6-code-inspection
Для того, чтобы запускать скрипты на ноде, надо установить nodejs плагин.
Preferences -> Plugins -> Browse Repositories -> ищем NodeJS
После чего можно будет ПКМ нажимать на .js скриптах и делать Run
