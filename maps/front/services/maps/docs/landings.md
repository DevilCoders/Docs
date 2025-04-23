# Лендинги

## Через [Landing Page Constructor](https://wiki.yandex-team.ru/lp-constructor/)

Обычное проксирование лендинга сделано на уровне балансера: [front-maps.slb.maps.yandex.net/lpc-landings](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.slb.maps.yandex.net/upstreams/list/lpc-landings/show).

При необходимости добавления новых путей:
1. Добавляем пути в указанный выше апстрим.
2. Поддержать эти пути в seourl, чтобы МЯК нормально резолвил эти пути: [`seourl/transform-seo-url.ts`](../src/server/seourl/transform-seo-url.ts).

Кроме того поддержаны лендинги, которые открыты только на **внутренних** пользователей. Схема следующая:

- С балансера запрос попадает в наше приложение.
- Проверяем авторизацию и привязку логина.
- Делает [внутренний редирект](https://www.nginx.com/resources/wiki/start/topics/examples/xsendfile/) в nginx.
- [Проксируем](https://wiki.yandex-team.ru/lpage-constructor/projects/creating/use-lp-on-custom-domain/#nginx) запрос в LPC.
