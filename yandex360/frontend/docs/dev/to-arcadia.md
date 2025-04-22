# Переезд в Arcadia


## Что поменялось

**CLI** `git` -> `arc` (очень [похож на git](https://docs.yandex-team.ru/devtools/src/arc/workflow))

**веб-интерфейс** `github.yandex-team.ru` -> `a.yandex-team.ru`
`.gitignore` -> `.arcignore`

## Что делать

* [Быстрый старт про акрадию](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
* [Прогнать плейбук](https://a.yandex-team.ru/arc_vcs/yandex360/frontend/tools/qyp/README.md)
* [Настроить shell](https://docs.yandex-team.ru/devtools/src/arc/config#shell)

Наша монорепа живет в `yandex360/frontend`.

```bash
cd ~/arcadia/yandex360/frontend
arc pull
npm ci # поставит зависимости в корне монорепы и husky-хуки
```

## Как работать

### настроить arc
Чтобы запретить коммит в транк, нужно добавить в конфиг `~/.arcconfig`:
```ini
[branch "trunk"]
    allowCommit = false
```

* Дока по arc: https://docs.yandex-team.ru/devtools/src/arc/workflow
* FAQ: https://wiki.yandex-team.ru/arcadia/arc/faq

### Как продолжить работать в аркадии в своей ветке из гита

```bash
cd
arc mount --allow-other
cd ~/arcadia/yandex360/frontend
npm ci

cd services/subscriptions

# переключиться в локальную ветк DARIA-70856, взяв ее из remote копии гитхаба
arc co -b DARIA-70856 external/github/personal-services/frontend/DARIA-70856
# trying to fetch remote branch 'external/github/personal-services/frontend/DARIA-70856'
# fetched branch 'external/github/personal-services/frontend/DARIA-70856'
# Switched to branch 'DARIA-70856'

arc br --unset-upstream
arc pull trunk
arc rebase trunk
# поправить конфликты, если есть (fix; arc add .; arc rebase --continue; repeat)
arc pr c --push --publish -m 'DARIA-70856: Редизайн экрана включения опт-ин'
```

### Где ссылки на тренбокс джобы

Вот они

![список проверок в PR](../images/checks.png =420x640)


### MQ, ревьюшница?

Больше нет. Ревьюеров назначает аркадия, либо можно добавить самостоятельно в интерфейсе.
Merge можно включить автоматический, произойдет после прохождения всех обязательных проверок.
Либо нажать кнопку "Merge".

`/ready` больше не работает


### Настроить фильтр в почте

![пример настройки фильтра](../images/mail-filters.png =792x147)


## При переезде потерялась итория / blame

DEVTOOLSSUPPORT-17950
ARC-2435
> `arc blame --full-topo`
> Планов доносить его до Арканума у нас нет.

если `--full-topo` не помогает
> Печально. Именно поэтому режим и называется экспериментальным. Нормальной починкой будем заниматься в привязанном тикете.


## Инструменты разработки

### Поддержка IDE

https://docs.yandex-team.ru/devtools/src/ide

Для те, кто пользуется WebStorm рекомендуется префетчить файлы проекта/проектов, над которыми будете работать для ускорения индексации, например:

```bash
arc prefetch-files ./services/liza
```

### Отображение названия ветки в консоли

[Нормальное решение](https://docs.yandex-team.ru/devtools/src/arc/config#shell)

Для тех, кто не ищет лёгких путей: добавить в `~/.bashrc` или аналог

```
function arc_branch() {
  branch=$(arc info --json 2>/dev/null | jq -r .branch)
  if [ -n "$branch" ]; then
    echo "($branch)"
  fi
}

# Дописать в нужное место `PS1`
PS1='...$(arc_branch)...'
```

## Стандартный флоу (на примере лизы)

### Фича

```bash
cd ~/arcadia/yandex360/frontend/services/liza
arc checkout trunk && arc pull # обновим транк
arc checkout -b DARIA-1234 # переключимся на ветку
# code code code
arc add .
arc commit -m 'DARIA-1234: commit message'

# оформляем PR:
# тут два способа
arc push -u users/$USER/DARIA-1234
arc pr create
# либо
arc pr create --push -m 'DARIA-1234: pull request description'

# команда выведет ссылку на пулл-реквест вида https://a.yandex-team.ru/review/2415036/details
# когда пулл создан, последующие коммиты можно просто пушить, они попадут в черновик PR, который в UI a.yandex-team.ru можно опубликовать

arc commit -a -m 'DARIA-1234: new commit message'
arc push # пушим в апстрим, в UI нужно опубликовать черновик

# пример с ребейзом
arc pull trunk # обновить транк
arc rebase trunk # можно добавить -i для интерактивного ребейза
arc push -f # пуш в апстрим с форсом
```


### Релиз

```bash
cd ~/arcadia/yandex360/frontend/services/liza
arc checkout trunk && arc pull # тянем свежий транк
arc checkout -b DARIA-12345 # переключаемся на релизную ветку
npm run package 40.0.0 DARIA-12345 # под капотом запушит в релизный апстрим `releases/psfront/liza/v40.0.0` - это замена тэгов в гите и откроет пулл-реквест в транк от ветки DARIA-12345
```

### Хотфикс

```bash
arc checkout -b hotfix-2 releases/psfront/liza/v38.0.1
arc cherri-pick {commit}
npm run package 38.1.0 DARIA-77777
arc pr create --push --publish # изменения должны попасть в транк
```

### Важные ветки или теги из гита

Ветки копируются в специальный префикс `external/github/personal-services/frontend/`
https://a.yandex-team.ru/arc_vcs/branches/?filterName=external%2Fgithub%2Fpersonal-services%2Ffrontend%2F

Теги в префикс `tags/external/github/personal-services/frontend/`
https://a.yandex-team.ru/arc_vcs/branches/?filterName=tags%2Fexternal%2Fgithub%2Fpersonal-services%2Ffrontend%2F


## CI

Переезжаем с трендбоксом, но будем двигаться в ((./new-ci New CI))

[мысли по поводу CI/CD](https://wiki.yandex-team.ru/users/avanes/new-ci/)

<details><summary>Дашборд</summary>
<iframe frameborder="0" width="100%" height="400px" src="https://charts.yandex-team.ru/preview/editor/qi4mxqpryboyj?showCountLabels=true&owner=PS-FRONTEND&project=YANDEX360%2FFRONTEND&flow=YANDEX360%2FFRONTEND%3A%3APR_FLOW&useTotalDuration=false&rangeDatepickerFrom=2022-04-08T00%3A00%3A00.000Z&rangeDatepickerTo=2022-04-15T20%3A15%3A30.353Z&showOwner=true&durationLimit=3600000&skipJunk=true&percentile=0.9&action=ACTION%3ACI&_embedded=1"></iframe>
<iframe frameborder="0" width="100%" height="600px" src="https://charts.yandex-team.ru/preview/editor/9xv3jv2rt2y02?project=YANDEX360%2FFRONTEND&owner=PS-FRONTEND&rangeDatepickerFrom=2022-04-14T00%3A00%3A00.000Z&rangeDatepickerTo=2022-04-15T20%3A15%3A30.344Z&showOwner=true&durationLimit=1200000&skipJunk=true&flow=YANDEX360%2FFRONTEND%3A%3APR_FLOW&action=ACTION%3ACI&_embedded=1"></iframe>
</details>


## Ссылки

[Система контроля версий arc](https://docs.yandex-team.ru/devtools/src/arc/workflow)
[«Инфра 2022: переезд в Аркадию». Видео и конспект встречи](https://clubs.at.yandex-team.ru/seminar/3841)
[Запись первой встречи про переезд с github в Аркадию](https://clubs.at.yandex-team.ru/verstka/7316)
[Запись второй встречи про переезд с github в Аркадию](https://clubs.at.yandex-team.ru/verstka/7331)
[Большой FAQ по аркадии](https://wiki.yandex-team.ru/arcadia/arc/faq)
