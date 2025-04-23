---
title: Интеграция с infra
---

## Зачем

Проброс релизов в infra позволит:

  - дежурным быстрее искать релизы своих и смежных сервисов
  - менеджерам - провязывать изменения метрик с релизами сервисов

## Куда смотреть?

  - [Namespace Путешествий в infra](https://infra.yandex-team.ru/services?filter=Travel&expand=collapseAll&isAllServices=true)
  - [Фильтр по текущим событиям Путешествий](https://infra.yandex-team.ru/timeline?preset=all&from=1637027163340&to=1637113563340&autorefresh=false&status=all&filter=travel&fullscreen=false)
  - [Дока по Infra](https://wiki.yandex-team.ru/infra/)

**Важно!** Не забываем выдать права TVM-приложению 2020685 (через IDM).
Роль нужна вот такая: infra.yandex-team.ru / Namespace / Namespace 'Travel' / {наш сервис в infra} / Дежурный


## Правила

Наше пространство имен - Travel.
Правило именования сервисов: travel-{service}-{project}, например travel-avia-shared-flights.
Правило именования окружений: окружения называем так же, как они называются у нас в Nanny / Deploy.

[Как включить экспорт релизов из Nanny/Deploy смотрим тут](https://wiki.yandex-team.ru/infra/#faq)


