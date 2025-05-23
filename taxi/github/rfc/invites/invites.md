**Название сервиса**

_invites_

**Какую продуктовую проблему решает сервис?**

Позволяет хранить информацию об участниках закрытого клуба, 
а также содержит механику вступления в закрытый клуб через инвайты.

**Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?**

Сейчас нет сервиса, который поддерживает механику закрытого клуба и инвайт-ссылок.

**Как именно сервис будет решать поставленные перед ним задачи?**

Сервис отвечает за хранение информации:
- о принадлежности пользователя к закрытому клубу
- список уникальных инвайт-ссылок для пользователей из закрытого клуба

Предоставляет набор ручек:
- `/invites/v1/membership`
- `/invites/v1/shortcuts`
- `/4.0/invites/v1/activate`

#### `/invites/v1/membership`
Проверить по _phone_id_, принадлежит ли пользователь к закрытому клубу.

Логика: 
1) смотрим в `invites.members` в какие активные клубы попадает текущий пользователь
2) смотрим в эксперименте `invites_secret_group` в какие клубы пользователю разрешено вступить
3) если в эксперименте есть клубы, которых нет в `invites.members`, то добавляем клубы (если их еще нет), пользователя в эти клубы, создаем инвайты и еще добавляем для этого пользователя тэг клуба в сервис taxi-tags
4) возвращаем список клубов пользователя (из `invites.members` и эксперимента)

Потребитель: persuggest (`/finalsuggest`) - [используем кэширование запросы в invites], 
т.е. сначала смотрим в кэш, если он говорит, что пользователь не из закрытого клуба, то делаем запрос в сервис invites и кэшируем

**Важно:** из-за срочности проекта самым простым и быстрым решением было врезаться в `/finalsuggest`, но у этого подхода есть недостатки:
- ручка `/finalsuggest` - блокирующая и чувствительная к времени ответа
- данные, которые отдаются в эксперименте, мало относятся к гео
Таким образом, решение об использовании ручки в `/finalsuggest` является временным, и в будущем будет перенесенно в другое место.

Фолбэк для потребителей: если сервис `invites` недоступен, то берем клубы из сервиса taxi-tags (через тонкий клиент)

Таким образом, если пользователь в клубе, то у него не будут мигать эксперементы из-за проблем с ручкой `/membership`, c другой стороны мы не кэшируем отсутствие клубов, что позволяет их включить моментально

#### `/invites/v1/shortcuts`
Для блендера отдаем шорткаты с инвайтами или их отсутствие.

Логика (с использованием LRU cache): 
1) смотрим инвайты в cache, если есть, то отдаем их
2) если нет в cache, то в из `invites.codes` достаем инвайты пользователя для активных клубов
3) распределяем инвайты по клубам в отдельные шорткаты
4) кладем полученные инвайты в cache и отдаем в response

Потребители: /v1/products (api-proxy)

Фолбэк для клиентов: если сервис недоступен, то пропадают шорткаты инвайтов

#### `/4.0/invites/v1/activate`
Активировать инвайт

Логика:
1) проверяем пользователя в `invites.members`
2) смотрим код в `invites.codes`

| Пользователь есть в `invites.members` | код в `invites.codes` | ответ |
|-|-|-|
| нет | нет кода | `code_invalid`|
| нет | код использован | `code_used`|
| нет | код не использован и старая версия приложения | `outdated_app` |
| нет | код не использован и старая версия ОС | `outdated_os` |
| нет | код не использован и прошла проверка приложения и ОС | `code_activated` |
| да | нет кода | `code_invalid`|
| да | код не использован или использован другим пользователем | `code_redudant`|
| да | код использовал текущий пользователь | `code_activated`|

Потребитель: клиенты дергают ручку при переходе по deeplink, ручка закрыта за Passanger Authorizer

**Разрабатывается один сервис или система?**

Один сервис

**С кем взаимодействует сервис?**

Потребители:
- persuggest: `/finalsuggest` (забрать информацию о принадлежности пользователя к закрытому клубу и прокинуть в кварги экспериментов)
- blender: source (отдавать информацию по инвайтам в шорткаты)
- клиенты (активировать инвайт)

**Какие базы использует?**

Одна postgress база.

**Какие периодические процессы?**

нет

**Какие данные и по какой схеме сервис будет хранить в базе?**

Таблица `invites.clubs` [id, name, is_active]
Таблица `members` [id, phone_id, club_id, created]
Таблица codes [id, code, creator_id, created_at, counsumer_id, activated_at]

**Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?**

members
- оценка объема сверху примерно 50% MAO - 13М записей: 128Б * 13M = 1.5ГБ
- 10% запись 2КБ/с 
- 90% чтение 20КБ/s

codes:
- оценка объема N * members = для 5 инвайтов - 8ГБ
- 10% запись: 10КБ/с
- 90% чтение 100КБ/с

**Какая нагрузка ожидается?**

- ручка активации - 10 RPS
- ручка проверки пользователя для закрытого клуба - 800 RPS
- ручка source для шорткатов - 1000 RPS

**Какие фолбеки предусмотрены на сам этот сервис?**

Проект инвайтов не влиет на основное флоу заказа, 
поэтому при проблема с сервисом пользователь не смогут увидеть onboarding, шорткат инвайтов, 
после восстановления сервиса пользователи смогу все равно увидеть все это.

Другими словам: фолбэк - отображение обычно интерфейса, без шорткатов.
 
**Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?**

Функциональность сервиса не влияет на основное флоу заказа такси, поэтому при недоступности сервиса отключается закрытый клуб, т.е. пользователи закрытого клуба вместо шорткатов увидят обычный главный экран.
 
**Какие точки отказа есть в сервисе?**

postgress

**Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить**

- количество участников закрытого клуба
- количество активаций в единицу времени

**Укажите технические метрики**

- размер базы данных
- время работы запросов в базу
- время работы ручек

**Активно ли будет изменяться сервис?**

Первоначально сервис будет запущен на 2 неделе, дальнейшие доработки возможны по запросу менеджеров.
