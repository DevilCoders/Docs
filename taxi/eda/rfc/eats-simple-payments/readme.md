
**Название сервиса**

eats-simple-payments

**Какую проблему решает**

Мы хотим вынести api v1 eats-payments в новый сервис, так как сейчас есть два api v1 и v2, которые сильно связаны большим количеством legacy кода, но при этом обладают разной логикой. v2 опирается на циклы заказов еды, при этом v1 позволяет совершать простые платежи не завязанные с едой. Также сейчас, благодаря b2b, будет увеличиваться количество пользователей api v1.

Подробнее про api v2: https://wiki.yandex-team.ru/eda/team/backend/platformteams/team-prime-time/proekty-komandy/revision-based-eats-payments-api/?from=%2Feda%2Fteam%2Fbackend%2Fteam-prime-time%2Fproekty-komandy%2Frevision-based-eats-payments-api%2F

**Основыне различия**
|               | v1            | v2    |
| ------------- |:-------------:| -----:|
| Состав заказа | Приходит в запросе | В запросе приходит revision id, с которым ходим в кору для получения состава заказа |
| Изменения заказа после оплаты | При каких-то измениях после оплаты, нужно создавать новый заказ | Состав заказа может поменяться |
| Чеки | Формируются на основе инвойса| Формируются на основе ревизий |

**API**

Остается без изменений, кроме поля revision, убрано из required, чтобы не создавать недопонимания, так как ревизии в v1 не используются, а как в роли токена идемпотентности будет выступать version.
