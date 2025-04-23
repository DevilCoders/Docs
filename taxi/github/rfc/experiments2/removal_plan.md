# План по закапыванию сервиса экспериментов2

## Ресурсы сервиса


## Пользователи сервиса

1. [b-cpp] Match - потребители: 3.0/promotions, 3.0/taxiontheway, fastcgi_model_context
   1. Мигрировать все живые эксперименты. Так как во всех местах, уже имеются как exp, так и exp3.
   2. Удалить старый код

2. [b-cpp] GetDriverExperiments - потребители: dp/t-o-c, dp/driver/authorization/login/new
   1. Добавить в компоненту ExperimentsComponent поддержку exp3
   2. Мигрировать активные эксперименты на exp3
   3. Удалить использование экспериментов2

3. [backend] banners.py, promo_stories
   1. Дождаться https://st.yandex-team.ru/GOALZ-84022
   2. Выпилить создание сторис с использованием exp2 (если ещё не будет сделано)

## Активные эксперименты

TODO
