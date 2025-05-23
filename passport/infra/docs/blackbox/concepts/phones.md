# Получение телефонов пользователя

К каждому пользовательскому аккаунту может быть привязано некоторое количество телефонов.

Информация о телефонах хранится в расширенных атрибутах аккаунта. У каждого телефона есть идентификатор `phone_id` и набор атрибутов телефона. Полный список атрибутов приведен в [документации Паспорта](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#section_kbk_b5f_2hb).

❗️ Информация о привязанных телефонах относится к персональным данным, поэтому большинство атрибутов **требуют специальных грантов для их чтения**.

{% note warning %}

По возможности не запрашивайте полные номера телефонов без крайней необходимости, используйте `phone_id` или маскированный телефонный номер.

{% endnote %}

Среди всех номеров телефонов один номер может быть привязан как защищённый. Этот номер требует ввода пароля для привязки и может использоваться для входа в аккаунт или восстановления доступа к аккаунту. В интерфейсе Паспорта он выделен зеленым.
Среди атрибутов этого номера выставлен атрибут 108 `phone.is_secured`.
Защищённого номера может не быть.

Также, среди всех номеров один номер может быть отмечен как номер для получения уведомлений. В интерфейсе Паспорта он отмечен колокольчиком. Если есть хотя бы один привязанный телефон, то какой-то один из них будет отмечен как номер для уведомлений. Он может совпадать с защищённым номером, а может и не совпадать.
Среди атрибутов этого номера выставлен атрибут 107 `phone.is_default`.

Если контекст вашей операции подразумевает безопасность, например, номер нужен для отправки пароля или кода подтверждения, нужно использовать защищённый номер телефона.
Если отправка смс информационная, например, рассылка или уведомление, лучше использовать номер для уведомлений.

## Аргумент getphones {#getphones}

Для получения телефонов, привязанных к аккаунту используется пара аргументов `getphones` и `phone_attributes`.

Аргумент `getphones` определяет, какие телефоны нужно выбрать. Поддерживаются значения `all` (выбрать все телефоны), и `bound` (выбрать только привязанные телефоны, т.е. те, которые были подтверждены пользователем).

Аргумент `phone_attributes` определяет, какие атрибуты телефонов нужно выбрать. Поддерживаемые значения - `all` (все атрибуты телефона) или список номеров атрибутов через запятую.
Если аргумент не передан или список пустой, то в ответе будет только список `phone_id`, без атрибутов телефонов.
Полный список атрибутов приведен [в таблице атрибутов телефонов](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#section_kbk_b5f_2hb)

Пример: в запрос добавляются параметры `getphones=all&phone_attributes=all`.
В ответе Черного ящика при этом появляется секция `phones`.
В XML:
```xml
<phones>
    <phone id="2">
        <attribute type="1">79161112233</attribute>
        <attribute type="101">+7 916 111‒22‒33</attribute>
        <attribute type="102">+79161112233</attribute>
        <attribute type="103">+7 916 ***‒**‒33</attribute>
        <attribute type="104">+7916*****33</attribute>
        <attribute type="105">1</attribute>
        <attribute type="108">1</attribute>
        <attribute type="2">1411571146</attribute>
        <attribute type="4">1411916746</attribute>
        <attribute type="6">1412183145</attribute>
    </phone>
    <phone id="3">
        <attribute type="1">79161111111</attribute>
        <attribute type="101">+7 916 111‒11‒11</attribute>
        <attribute type="102">+79161111111</attribute>
        <attribute type="103">+7 916 ***‒**‒11</attribute>
        <attribute type="104">+7916*****11</attribute>
        <attribute type="2">1412442345</attribute>
    </phone>
</phones>
```
В json:
```json
     "phones" : [
        {
           "attributes" : {
              "101" : "+7 916 111‒22‒33",
              "1" : "79161112233",
              "105" : "1",
              "4" : "1411916746",
              "104" : "+7916*****33",
              "102" : "+79161112233",
              "2" : "1411571146",
              "108" : "1",
              "103" : "+7 916 ***‒**‒33",
              "6" : "1412183145"
           },
           "id" : "2"
        },
        {
           "attributes" : {
              "102" : "+79161111111",
              "2" : "1412442345",
              "1" : "79161111111",
              "101" : "+7 916 111‒11‒11",
              "104" : "+7916*****11",
              "103" : "+7 916 ***‒**‒11"
           },
           "id" : "3"
        }
     ]
```
