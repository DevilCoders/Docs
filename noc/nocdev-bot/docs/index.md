# Назначение
`nocdev-bot` автоматизирует рутинные задачи, связанные с st, abc и т.п., которые не получается автоматизировать штатными средствами этих сервисов.

# Функциональность
Функциональность можно разделить на [Agile](#agile), [Дежурства](#дежурства) и [Telegram](#telegram).

## Agile

`nocdev-bot` занимается ротацией спринтов:
* по формуле рассчитывает номер текущего спринта
* из ST получает [активный спринт](https://st.yandex-team.ru/agile/board/9191/sprints) и, если нужна ротация, то закрывает активный спринт и берёт текущий в работу
* создает спринты на будущее (`TODO: subj`)

## Дежурства

`nocdev-bot` занимается:
* назначением исполнителей для тикетов:
  * получает текущих дежурных NOCDEV из [ABC](https://abc.yandex-team.ru/services/NOCDEV/duty/)
  * получает задачи без исполнителя из [NOCDEVDUTY](http://st.yandex-team.ru/NOCDEVDUTY) и [NOCREQUESTS](http://st.yandex-team.ru/NOCREQUESTS), пытается определить к какому дежурному эта задача относится и либо выставляет определенного дежурного исполнителем, либо призывает дежурных и сообщает о невозможности определения
* ротирует недельный [тикет-отчет](https://st.yandex-team.ru/NOCDEVDUTY/filter?resolution=empty()&components=94328) про дежурства: закрывает тикет за предыдущую неделю, а в тикете за текущие неделю добавляет номер спринта в заголовок

## Telegram
Пока нет.
```
TODO: добавить описание, когда функциональность будет сформулирвоана и запущена
```

# Код
Код находится в [arcadia/noc/nocdev-bot](https://a.yandex-team.ru/arc/trunk/arcadia/noc/nocdev-bot)

# Эксплуатация
В проекте настроен [Arcadia CI](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fnocdev-bot&id=nocdev-bot-release), который автоматически собирает и деплоит проект после каждого коммита в директорию.
Инсталляция развернута в [deploy](https://deploy.yandex-team.ru/stages/nocdev-bot).
