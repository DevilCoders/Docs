# Флоу постоплатника


## Регистрация

{% note info "Важно про регистрацию постоплатников" %}

* **регистрация постоплатников в проде невозможна на уровне бэкенда**
* зарегистрировать постоплатника можно только на престейбле и только со специальными параметрами

{% endnote %}


### Регистрация постоплатника на престейбле

* завести нового пользователя
* перейти по ссылке https://admin2.dsp.yandex.ru/register?product=org_mail_pro_premium3000_wo_trial&from=promo&promo=mail360&noredirect=1 (ключевые тут параметры `product` && `noredirect`)
* заполнить реквизиты организации. Данные можно [сгенерировать тут](http://mellarius.ru/random-data)
* нажать на кнопку "Зарегистрировать" на форме реквизитов
* в админке проверить, что подключен "Профессиональный" тариф


## Создание 2+ организации

* из админки через селект выбора организации || на странице выбора организации (`/select-organization`) создать новую организацию
* новой созданной организации доступны **постоплатные тарифы**

{% note info "Про тарифы 2+ организаций постоплатников" %}

* если, хотя бы в одной организации постоплатника, включен постоплатный тариф, то все последующие созданные организации буду иметь постоплатные тарифы
* постоплатника могут пригласть администраторов в организацию с предоплатыми тарифами и он сможет подключать/отключать их

{% endnote %}
