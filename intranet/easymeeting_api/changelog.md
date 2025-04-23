0.48
----
 * EASYMEETING-207 Обновил ylog для поддержки уровня лога в Deploy  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/295766e ]

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2020-06-17 18:54:57+03:00

0.47
----
 * EASYMEETING-207 fix release.hjson  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/591d10d ]

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2020-06-17 16:35:54+03:00

0.46
----
 * EASYMEETING-207 Обновил конфиг releaser и readme для Deploy (#66)  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/17e8b05 ]

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2020-06-17 16:07:46+03:00

0.45
----
 * EASYMEET-205 Перевоз в Deploy (#65)  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/e8ddb1c ]

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2020-05-19 19:27:24+03:00

0.44
----
 * EASYMEET-183 Поддержали TVM2 и ходим в календарь по нему (#63)  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/3a37f3f ]

* Избавились от django-ids
* Отказались от ручки календаря get-user-settings в пользу staff-api
* Фикс версии django_appconf==1.0.2 как последней для Py2
* В staff-api ходим по tvm2
* Рефакторинг
* Поддержали запись кассет для тестов со стенда

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2020-04-15 18:18:06+03:00

0.43
----
 * Доработка для ручки ping  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/2fa677a ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2020-03-24 13:08:02+03:00

0.42
----
 * Ручка ping      [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/94cc808 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2020-03-23 19:42:32+03:00

0.41
----
 * Trendbox                                                                                 [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/8644419 ]
 * Собираем локально через docker-compose                                                   [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/f0077f7 ]
 * EASYMEET-190: При поиске переговорок получаем инфу о встрчах от лица всемогущего робота  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/d18b2dc ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2020-03-20 14:01:46+03:00

0.40
----
 * EASYMEET-174 Обновил тестинг календаря еще раз  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/6400897 ]

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2019-12-25 16:08:34+03:00

0.39
----
 * EASYMEET-174 Обновил тестинг календаря                                 [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/7dfe62c ]
 * EASYMEET-174 Исключаем переговорки из доступных на время restrictions  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/240e72d ]

[Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru) 2019-12-24 15:24:22+03:00

0.38
----

* [Mikhail Agranovskiy](http://staff/agrml@yandex-team.ru)

 * EASYMEET-163 Перевел сервис на хождение в PGaaS напрямую  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/279012a ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-08-21 18:09:50+03:00

0.37
----
 * EASYMEET-149: Удалил ненужные конфиги локов  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/d172818 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-01-24 13:38:17+03:00

0.36
----
 * EASYMEET-125: В ручке деталей встречи исключаем участников без логина  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/dd9cb42 ]
 * EASYMEET-110: Создание встреч без переговорок                          [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/7c5ddec ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-09-18 15:10:16+03:00

0.35
----
 * EASYMEET-121: Пропускаем выходные в /personsFreeIntervals  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/69f28f4 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-08-23 16:36:00+03:00

0.34
----
 * EASYMEET-107: Поправил тесты                  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/bbcacdf ]
 * EASYMEET-107: Отдаем в ручке офисов tzOffset  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/697bb6e ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-08-21 14:54:37+03:00

0.33
----
 * EASYMEET-107: Получаем события от календаря в UTC  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/7a09ada ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-08-16 15:30:36+03:00

0.32
----
 * EASYMEET-107: Дополнительные параметры в ручке             [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/7fc5f25 ]
 * EASYMEET-107: Переименовал nearest в personsFreeIntervals  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/694b15c ]
 * EASYMEET-107: Ручка поиска свободного времени участников   [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/029940b ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-08-06 15:32:17+03:00

0.31
----

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * Добавил правильную версию pyyaml в зависимости  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/bcb2c68 ]

* [christina ilyenko](http://staff/chrighter@yandex-team.ru)

 * Поправили заголовки в кассетах                            [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/56591e4 ]
 * EASYMEET-106 поправили ручку офисов для нового селектора  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/7332e5b ]

[christina ilyenko](http://staff/chrighter@yandex-team.ru) 2018-07-31 14:23:26+05:00

0.30
----
 * EASYMEET-53: Задублировался суффикс  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/5181b38 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-25 19:20:35+05:00

0.29
----
 * EASYMEET-53: Пустые значения имени и описания  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/5028927 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-25 15:43:58+05:00

0.28
----
 * Увеличил тайминги до всех сервисов вдвое          [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/de756d6 ]
 * Не показываем форму обратной связи слишком часто  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/64909aa ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-21 18:31:57+05:00

0.27
----
 * EASYMEET-53: Ручка создания пачки встреч  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/e8a6334 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-21 11:45:56+05:00

0.26
----
 * EASYMEET-58: Обработка False значения при оценке визита  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/eaa6ab1 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-14 15:45:48+05:00

0.25
----
 * EASYMEET-85: Правильное распределение сотрудников по офисам  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/440fbd0 ]
 * EASYMEET-58: Сохранение данных визита                        [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/b2dbef9 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-14 14:42:14+05:00

0.24
----
 * EASYMEET-74: Увеличил количество сотрудников в ответе          [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/acb02c7 ]
 * EASYMEET-74: Добавил сортировку при обращении к апи стаффа за сотрудниками  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/3896527 ]
 * EASYMEET-77: Объединить ручки /persons и /gaps                 [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/87e1cac ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-05-03 11:40:49+05:00

0.23
----
 * Обработка приватных встреч  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/e5b886c ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-04-18 14:02:40+05:00

0.22
----
 * EASYMEET-47: Считаю уволенных сотрудников в отсутствиях         [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/34545ba ]
 * EASYMEET-54: При вычислении отсутствия учитываем "родной" офис  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/ece0ba0 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-04-18 11:02:19+05:00

0.21
----
 * EASYMEET-55: Удалить дубликаты комбинаций (#32)  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/060a7ee ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-04-11 11:38:54+03:00

0.20
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * EASYMEET-20: Cочетания переговорок (#31)    [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/64fa416 ]

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * EASYMEET-29: Получение приватного события  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/fddc609 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-29 14:18:13+03:00

0.19
----
 * EASYMEET-44: Разделил persons_availability по городам  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/dd2ad1b ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-27 20:27:04+05:00

0.18
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Refactored RoomSlot class  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/ec12edd ]

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * EASYMEET-23: Не учитываем людей, которые отказались от встречи  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/1d73849 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-27 13:58:04+05:00

0.17
----
 * EASYMEET-29: 414 ошибки от календаря                                 [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/2ce8db1 ]
 * EASYMEET-23: Учитываю ответ пользователя на приглашение              [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/1d68611 ]
 * EASYMEET-23: Рефакторинг, возвращаю больше информации о людях        [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/a0e2f5d ]
 * EASYMEET-36: Объединил офисы "Красной розы" при подсчете отсутствий  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/50fe5b0 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-26 19:54:47+05:00

0.16
----

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Fix Person.is_staff for production  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/9c743cc ]
 * Add pgaas host in README            [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/35eaa7d ]

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * EASYMEET-36: Учитывать занятость только сотрудников в данном офисе  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/bb8c9b8 ]
 * EASYMEET-25: Добавил кеширование запроса за переговорками           [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/b904ab9 ]
 * EASYMEET-25: Убрал недоступные для бронирования переговорки         [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/95aea88 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-23 19:01:21+05:00

0.15
----
 * Fix core initial migration               [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/3490500 ]
 * Django-админка + скрипт создания офисов  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/3aa1a93 ]
 * Набросок модели офиса + миграция         [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/ed167c2 ]
 * EASYMEET-35: Настроить базу данных       [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/55dd989 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-03-22 19:06:06+03:00

0.14
----
 * EASYMEET-27: Добавил eventId в ручку комбинаций  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/83cc0ba ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-22 14:43:54+05:00

0.13
----
 * EASYMEET-27: Ручка подробной информации о событии  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/6d546a7 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-22 11:23:48+05:00

0.12
----
 * EASYMEET-28: Добавил фактор количества переходов                        [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/1a85f53 ]
 * EASYMEET-28: Инвертировал значение факторов                             [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/413bc9f ]
 * EASYMEET-29: Безопасное обращение к полям от календаря. Таймауты 4 сек  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/1cc4042 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-19 17:43:15+05:00

0.11
----
 * EASYMEET-23: Несколько запросов к gap  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/f3e51c1 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-16 13:37:57+05:00

0.10
----
 * EASYMEET-23: Проверка на наличие логина  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/72ebb6f ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-15 18:29:52+05:00

0.9
---
 * EASYMEET-22: Изменил формат в поле дат ручки /combinations  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/88b6a08 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-15 17:13:01+05:00

0.8
---

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-15 11:01:37+05:00

0.7
---
 * EASYMEET-24: Добавил attrs             [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/b0bb2ab ]
 * EASYMEET-24: Занятость людей           [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/fd8434c ]
 * EASYMEET-23: Фактор доступности людей  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/fcb73c9 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-03-15 10:56:22+05:00

0.6
---

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * EASYMEET-17: Ручка отсутствий по списку людей  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/51b01d0 ]

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * EASYMEET-15: Ручка информации о сотрудниках  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/6246c3a ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-02-21 16:41:27+05:00

0.5
---

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * EASYMEET-18: Ручка, предлагающая варианты переговорок  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/da4862e ]

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * EASYMEET-16: Добавил кэширование                                        [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/f66d779 ]
 * EASYMEET-16: Переписал ручку списка офисов со стафф апи на календарное  [ https://github.yandex-team.ru/easymeeting/easymeeting-api/commit/4045458 ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-02-20 15:25:35+03:00

0.4
---

* [Kirill Sibirev](http://staff/sibirev@yandex-team.ru)

 * Enable list for json responses  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/f1ac220 ]

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * EASYMEET-16: Сериалайзер для ручки списка офисов   [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/d4159a0 ]
 * EASYMEET-16: Разделил view по разным модулям       [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/1772cdf ]
 * EASYMEET-16: Ручка со списком всех офисов Яндекса  [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/b82beff ]
 * Добавили staff в зависимости в README              [ https://github.yandex-team.ru/easymeeting/easymeeting/commit/4e890b2 ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-02-15 12:37:31+05:00

0.3
---

* [Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru)

 * Поправил порядок запуска тестов  [ https://github.yandex-team.ru/tools/easymeeting/commit/299c986 ]
 * EASYMEET-14: Ручка информации о переговорках  [ https://github.yandex-team.ru/tools/easymeeting/commit/2a1fd5b ]

[Sergey Zhigalov](http://staff/zhigalov@yandex-team.ru) 2018-02-13 16:10:13+05:00

0.2
---
 * Набросок похода в календарь  [ https://github.yandex-team.ru/tools/easymeeting/commit/143641e ]

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-23 22:01:44+03:00

0.1
---
  * Initial

[Kirill Sibirev](http://staff/sibirev@yandex-team.ru) 2018-01-16 14:43:29+03:00

