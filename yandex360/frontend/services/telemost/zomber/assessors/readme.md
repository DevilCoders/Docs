#Зомбико-генератор для тестирования

Как выглядит:
https://jing.yandex-team.ru/files/maksimbark/2020-06-03_20.39.57-browser_Wobbly-Starling.png

Форма для запуска:
http://maksimbark-dev.sas.yp-c.yandex.net:3000/zomb
или можно воспользоваться расширением для браузера https://github.yandex-team.ru/maksimbark/zomb-chrome-extension

Команда для запуска:  
`stand=telemost.dsp conf=123 zombname=qwe mute=yes lifetime=2 npx wdio run wdio.conf.js`

`telemost.dsp` - стенд. К передпнному значению будет добавлено `.yandex.ru` 
`123` - номер конференции  
`qwe` - имя зомбика  
`mute` - `yes`/`no`: нажать ли кнопку мьюта после входа в конференцию
`lifetime` - от 1 до 30, время жизни зомбика в минутах

Для запуска нескольких зомбиков можно воспользоваться циклом на bash:
```
#!/bin/bash
for ((i=1; i < 10; i++))
do
conf=123 zombname=qwe mute=yes lifetime=2 npx wdio run wdio.conf.js &
done
```