### Общеяндексовые учения по закрытию локаций с помощью HBF

Если обычные ([понедельничные](https://docs.yandex-team.ru/marty/training/monday) и [пятничные](https://docs.yandex-team.ru/marty/training/friday)) проходят на уровне закрытия балансерами - фактически, мы закрываем трафик на уровне L7, - то эти учения мы проводим на уровне L3-L4: датацентр закрывается на уровне сети.
Ещё одно отличие - такие учения проводятся только в одном ДЦ за раз.

## Подготовка

За сутки до проведения работ необходимо выполнить несколько подготовительных действий. Они одинаковы и для работ, и для учений.


Галочка | Действие
--: | :---
<input type="checkbox" /> | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN):
~                         |```{{ msg_1 }}```
<input type="checkbox" /> | Запустить Жёлтый протокол, назвать чат ```Учения в {ДЦ} {дата}```
<input type="checkbox" /> | Уточнить, кто будет снимать анонсы L3: Сообщение в чат [Регламентные работы и учения - организаторы]: ```Коллеги, а кто завтра от Traffic Team будет с нами на учениях?```



#### Пошаговая инструкция
{% list tabs %}
- Учения
    Галочка | Минут от начала | Действие
    --: | ---: | :---
    <input type="checkbox" /> | -60 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Через час начинаем учения по закрытию ДЦ /SAS/MAN/VLA`
    <input type="checkbox" /> | -60 | Ставим фриз релизов в [rviewer](https://rviewer.yandex-team.ru/schedule)
    <input type="checkbox" /> | -60 | Заводим [preset](https://firewall.yandex-team.ru/drills). Проект - `_YANDEXNETS_`. Остальные поля интуитивно понятны
    <input type="checkbox" /> | -17 | [Ставим ДТ](https://juggler.yandex-team.ru/dashboards/downtimer/) на поиск
    <input type="checkbox" /> | -16 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Закрываем поиск`
    <input type="checkbox" /> | -15 | Закрываем [L7](https://nanny.yandex-team.ru/ui/#/list-l7heavy/)
    <input type="checkbox" /> | -10 | Закрываем [сервисные](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/)
    <input type="checkbox" /> | -5 | Снимаем [анонсы L7](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 0 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Поиск закрыт`
    <input type="checkbox" /> | 1 | Ставим ДТ на [локацию](https://juggler.yandex-team.ru/dashboards/drills_downtimer/)
    <input type="checkbox" /> | 2 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `ДТ выставлен. Снимаем анонсы L3.`
    <input type="checkbox" /> | 5 | Просим коллег из TT в чате работ снять анонс L3 SLB
    <input type="checkbox" /> | 10 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `L3 SLB снят, ждём 10 минут`
    <input type="checkbox" /> | 20 | Закрываем [HBF](https://firewall.yandex-team.ru/drills/presets/)
    <input type="checkbox" /> | 20 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `HBF закрыт, ждём 30 минут`
    <input type="checkbox" /> | 20 | Ждём 30 минут
    <input type="checkbox" /> | 50 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Открываем HBF`
    <input type="checkbox" /> | 50 | Открываем [HBF](https://firewall.yandex-team.ru/drills/presets/)
    <input type="checkbox" /> | 55 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `HBF открыт, возвращаем L3 SLB`
    <input type="checkbox" /> | 55 | Просим коллег из TT вернуть анонс L3 SLB
    <input type="checkbox" /> | 60 | Снимаем ДТ с [локации](https://juggler.yandex-team.ru/dashboards/drills_downtimer/)
    <input type="checkbox" /> | 65 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Открываем поиск`
    <input type="checkbox" /> | 65 | Возвращаем [анонсы L7](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 68 | Открываем [сервисные](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/)
    <input type="checkbox" /> | 70 | Наливаем 5% в  [production_search/main](https://nanny.yandex-team.ru/ui/#/l7heavy/production_search)
    <input type="checkbox" /> | 72 | Наливаем 15% в  [production_search/main](https://nanny.yandex-team.ru/ui/#/l7heavy/production_search)
    <input type="checkbox" /> | 75 | Прожимаем defolt на [L7](https://nanny.yandex-team.ru/ui/#/list-l7heavy/)
    <input type="checkbox" /> | 77 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Поиск открыт, сервисы могут возвращать нагрузку`
    <input type="checkbox" /> | 80 | Ставим ДТ с [поиска](https://juggler.yandex-team.ru/dashboards/downtimer/)
    <input type="checkbox" /> | 80 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN):
    ~ | 80 | `{{ msg_2 }}`

- Работы

    **Это копия действий из вкладки "Учения", тут указаны не все пункты. Надо доделывать**
    Галочка | Минут от начала | Действие
    --: | ---: | :---
    <input type="checkbox" /> | -сутки | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Коллеги, привет!  Напоминаем, что завтра /подставить дату/ состоятся учения в ДЦ /SAS/MAN/VLA. Начало учений в /подставить время/. Пожалуйста, снимите нагрузку со своих сервисов к этому времени.`
    <input type="checkbox" /> | -сутки | Сообщение в чат [Регламентные работы и учения - организаторы]: `Коллеги, а кто завтра от Traffic Team будет с нами на учениях?`
    <input type="checkbox" /> | -60 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Через час начинаем учения по закрытию ДЦ /SAS/MAN/VLA`
    <input type="checkbox" /> | -60 | Ставим фриз релизов в [rviewer](https://rviewer.yandex-team.ru/schedule)
    <input type="checkbox" /> | -60 | Заводим [preset](https://firewall.yandex-team.ru/drills)
    <input type="checkbox" /> | -17 | Ставим ДТ на [поиск](https://juggler.yandex-team.ru/dashboards/downtimer/)
    <input type="checkbox" /> | -16 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Закрываем поиск`
    <input type="checkbox" /> | -15 | Закрываем [L7](https://nanny.yandex-team.ru/ui/#/list-l7heavy/)
    <input type="checkbox" /> | -10 | Закрываем [сервисные](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/)
    <input type="checkbox" /> | -5 | Снимаем [анонсы L7](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 0 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Поиск закрыт`
    <input type="checkbox" /> | 1 | Ставим ДТ на [локацию](https://juggler.yandex-team.ru/dashboards/drills_downtimer/)
    <input type="checkbox" /> | 5 | Просим коллег из TT снять анонс L3 SLB
    <input type="checkbox" /> | 10 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `L3 SLB снят, ждём 10 минут`
    <input type="checkbox" /> | 20 | Закрываем [HBF](https://firewall.yandex-team.ru/drills/presets/)
    <input type="checkbox" /> | 20 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `HBF закрыт, ждём 30 минут`
    <input type="checkbox" /> | 50 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Открываем HBF`
    <input type="checkbox" /> | 50 | Открываем [HBF](https://firewall.yandex-team.ru/drills/presets/)
    <input type="checkbox" /> | 55 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `HBF открыт, возвращаем L3 SLB`
    <input type="checkbox" /> | 55 | Просим коллег из TT вернуть анонс L3 SLB
    <input type="checkbox" /> | 60 | Снимаем ДТ с [локации](https://juggler.yandex-team.ru/dashboards/drills_downtimer/)
    <input type="checkbox" /> | 65 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Открываем поиск`
    <input type="checkbox" /> | 65 | Возвращаем [анонсы L7](https://nanny.yandex-team.ru/ui/#/its/locations/l7_heavy/l3_checks/)
    <input type="checkbox" /> | 68 | Открываем [сервисные](https://nanny.yandex-team.ru/ui/#/its/locations/balancer/all-service/)
    <input type="checkbox" /> | 70 | Наливаем 5% в  [production_search/main](https://nanny.yandex-team.ru/ui/#/l7heavy/production_search)
    <input type="checkbox" /> | 72 | Наливаем 15% в  [production_search/main](https://nanny.yandex-team.ru/ui/#/l7heavy/production_search)
    <input type="checkbox" /> | 75 | Прожимаем defolt на [L7](https://nanny.yandex-team.ru/ui/#/list-l7heavy/)
    <input type="checkbox" /> | 77 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `Поиск открыт, сервисы могут возвращать нагрузку`
    <input type="checkbox" /> | 80 | Ставим ДТ с [поиска](https://juggler.yandex-team.ru/dashboards/downtimer/)
    <input type="checkbox" /> | 80 | Сообщение в чат [Регламентные работы и учения ДЦ](https://t.me/joinchat/PaZhvX5pm5phcPFN): `На этом сегодняшние учения в /SAS/MAN/VlA/ закончены. Прошу приносить все выявленные проблемы в тикет /ссылка на тикет/. Всем спасибо. Список дальнейших учений, как обычно, смотрите тут: https://st.yandex-team.ru/DRILLS-2`
{% endlist %}
