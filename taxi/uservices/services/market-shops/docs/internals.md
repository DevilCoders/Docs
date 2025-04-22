# Что под капотом
Сервис написан под userver с помощью автогенерации.

## Архитектура

<iframe frameborder="0" width="100%" height="217px" src="https://drawio.yandex-team.ru?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=market-shops-arch#R7Vhdb9sgFP01eazk79iPiZu0k1ZpUytV2hu1ic2KjUfIR%2FfrdzEQ47jNsqpbo6x5IHDuxVwO9x6TjPy02l5x1JQ3LMd05Dn5duRfjjzP9SMHviTypJAkDBRQcJJrpw64JT%2BxBvW8YkVyvOw5CsaoIE0fzFhd40z0MMQ52%2FTdFoz2V21QgQfAbYboEL0nuSgVGntRh19jUpRmZTdKlOUBZY8FZ6tar1ezGitLhcxj9B6XJcrZxoL82chPOWNC9aptiqmk1TCm5s1fsO5C5rgWx0yYfru84vfJJP%2Fq4mJD0GZ%2BhS%2FG6ilrRFeaCh2seDLc4Byo0kPGRckKViM669Bpu38sl3Fg1Pl8ZqwB0AXwOxbiSZ87WgkGUCkqqq1qTbnQi3vT0JKteIYPbMhkD%2BIFFgf8vN0JQFJjVmHBn2AexxQJsu7HgXR2FTu%2FjmboaKb%2FgHV3wPrN9NNIZpvvSgpHQOQ0aFunbS9N645iZQ0H57QpicC3DWrp2UCdwoMQJUUNwwx4xByANeaCQN5PtKEied6e4YLVwpyyPJKl4OxxVwy%2B9CCUpowy3i7nz%2BGTpnoj8FS8PXx2Q671BF%2FXh5aOWA83XR26xqW0atD4vfnhxOdWEt6RJeG%2FZ0l4z7AeUQh32vS4j36spGBOK9gNgQyegNVpttC2pDkKvxCSZmkLLBvkqLjQJSFtuip65hxnjMN%2BmfaRx8gpkapuloZeob%2FbAGWp1MUOhRNP5m2Nzqw69g0CFexZVtWf6Fr3nN%2BVPrShWfiB74cC1O9F0xmafawcTH8V1RQvhDLG0jhgSfKRmg1B%2BI6149Diw1a35FDcfyvKaWwRHpj4VKwQmWvtwbNO03k%2B1j3JeFF4BxLNwHVB25uClFyjzUooXE%2BP56giVErmNaZrLB%2Fd149OgNzXqPsseiN1d5MTk%2Ffk3OTdP1Leg%2FeUd%2F%2Bs5D2wyt%2B1BMH5PyT9BvFHSDXPmWQZXi4%2F9O%2FQ7TaIT0v%2FzE%2Fu8xHA4EgBDN9TAIMh672L0e6KqPrjwYVk73qk3FLLbWLdrmbWjSW0cM%2F4t9Zz%2BQUZuid2xwjP6m0XW%2Fnn9VMKWvuinJjEst9zjuWsUjzS%2FdN9w13f3X1pd2FHDu3YerXHH%2B%2B9AzUZjf9ZTcKw%2Bxe1tVn%2FUvuzXw%3D%3D"></iframe>

Индексатор параллельно с варкой индекса собирает и обогащает болшое количество файлов под репорт (report-data). Среди них имеется мнжество файлов из разных источников, содержащие данные о магазинах. Некоторое множество этих файлов публикуется в виде ресурса в [Market Access](https://wiki.yandex-team.ru/market/report/infra/shiny.access/).
Сервис запускает Access Updater, который периодически скачивает новую версию ресурса. Далее файлы загружаются (используется имеющийся код из репорта) в ОЗУ. Обработчики ручек парсят запросы и отдают данные по магазинам.

## Логи
[Описание и последовательность действий](https://wiki.yandex-team.ru/market/report/infra/shop/logs)
