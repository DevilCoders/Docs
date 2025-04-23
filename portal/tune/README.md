[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=portal/tune&vcs=arc)](https://oko.yandex-team.ru/arc/portal/tune)

[Вики](https://wiki.yandex-team.ru/morda/tune/)

## How to release
1. `make release`
2. Создаётся ((https://st.yandex-team.ru/HOME/filter?tags=urelease%3Atune&resolution=empty() релизный таск)), собирается пакет, автоматически выкатывается в тестинг
3. Протестировать - l7test.yandex.ru/tune etc.
4. По календарю и ((https://infra.yandex-team.ru/timeline таймлайну)) проверить, что в дц не проводится никаких работ и общеяндексовых проблем
4. В релизный таск перевести в статус "Выкладывается"
4. Жмакнуть `release` в sandbox таске "deploy" (ссылка в релизном таске называется Nanny deploy)
5. Пойти на дашборд https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/tune/
6. Нажать в дашборе `select` затем `commit`
7. `Deploy` в верхнем ряде кнопок
8. открыть панель мониторинга https://yasm.yandex-team.ru/panel/portal_tune и графики тюна на ((https://dash.yandex-team.ru/1ommkfbscurqz?tab=aY дашборде фронтенда))
9. дождаться деплоя, по очереди активируя шаги (кнопка Start около блоков с пальцем вверх). Первый шаг - престейбл, ждём, смотрим графики. Второй - выкатка на всё


## How to develop

```
sudo mkdir /opt/www/tune-d{номер инстанса}
sudo chown $USER /opt/www/tune-d{номер инстанса}
git clone git@github.yandex-team.ru:morda/tune.git /opt/www/tune-d{номер инстанса}
cd /opt/www/tune-d{номер инстанса}
make dev #запускает сборку и сервисы
make start #или ./debugstart.sh для автоматического перезапуска ноды при изменениях.
```
Дев-стенд тюна доступен будет по адресу https://tune-v101d0.wdevx.yandex.ru/, где
v101 — номер машинки
d0 — номер инстанса тюна.

для автопересборки бандлов при изменениях:
%%
cd tmpl
make webpack-watch
%%
