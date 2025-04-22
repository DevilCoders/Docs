# Скрипт для генерации входных данных приёмки

1) Находим прошлый и текущий релизы на дашборде - https://st.yandex-team.ru/dashboard/24351
2) Копируем содержимое `meta.json` из прошлого релиза в файл `current_release_meta.json`
3) Копируем содержимое `meta.json` из текущего релиза в файл `new_release_meta.json`
4) Запускаем `node index.js`

Получаем:

```
2021-04-27
Files watch.js:
bundle prod, new-counter-experiment
503 bx1nzewshyqnl6k,bx1nzewshyqnldo
  vs
bundle preprod
510 bx3m23xb11t1tks
Click to generate report - http://analytics-metrika.man.yp-c.yandex.net/code_versions?date=2021-04-27&code_version_prod=503&code_version_preprod=510&code_features_prod=bx1nzewshyqnl6k,bx1nzewshyqnldo&code_features_preprod=bx3m23xb11t1tks&type_of=watch
-----
2021-04-27
Files tag_turbo.js:
bundle prod, new-counter-experiment
503 21fptk9d82rcgzlc,21fptk9d82rcgzsg
  vs
bundle preprod
510 21frrmydqluev7zk
Click to generate report - http://analytics-metrika.man.yp-c.yandex.net/code_versions?date=2021-04-27&code_version_prod=503&code_version_preprod=510&code_features_prod=21fptk9d82rcgzlc,21fptk9d82rcgzsg&code_features_preprod=21frrmydqluev7zk&type_of=new_counter
-----
2021-04-27
Files tag.js:
bundle prod, new-counter-experiment
503 5gv0p5rfuji4o8hq,5gv0p5rfuji4o8ou
  vs
bundle preprod
510 5gv2n8ggd2l72gvy
Click to generate report - http://analytics-metrika.man.yp-c.yandex.net/code_versions?date=2021-04-27&code_version_prod=503&code_version_preprod=510&code_features_prod=5gv0p5rfuji4o8hq,5gv0p5rfuji4o8ou&code_features_preprod=5gv2n8ggd2l72gvy&type_of=tag
-----
```
