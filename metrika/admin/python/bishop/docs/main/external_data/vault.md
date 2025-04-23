### Vault

#### Описание
В словаре `vault` находятся данные о секретах, полученные из Yandex Vault (https://yav.yandex-team.ru)

{% cut "Пример словаря" %}
```python
vault = {
    "sec-01ckbpeeq0926ty0rmz2jn5jy4": "ver-01e20d0n56j1c4dy39mm6jzv2y",
    "sec-01ckx62bkvpee201ks4d4a1g09": "ver-01ckx62bm2j00f44sag2910hn4",
    "sec-01cmtcz53m3xe6rqs51tfyyh94": "ver-01e1cj41kragzj58pjgapzbctj",
}
```
{% endcut %}

#### Переодичность обновления
На момент написания составляет 10 минут. Уточнить значение можно в [конфиге](https://bishop.mtrs.yandex-team.ru/program/bishop-helper/config/metrika.deploy.infra.bishop.helper.production/active) bishop-helper.

#### Получение данных
Для получения данных robot-metrika-bishop должен иметь доступ на чтение к секрету. Bishop сохраняет к себе все секреты (пары secret uuid/version uuid) до которых у него есть доступ.
