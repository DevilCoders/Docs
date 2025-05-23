# Про sustain в Биллинге Маркета

Здесь собираем всю информацию о sustain-е

## Что это вообще такое

_Sustain_ - это, дословно, "поддерживать", "укреплять", "сохранять". Вот этим и занимается подразделение састейна.
Еще можно понимать так: подразделение састейна обеспечивает _sustainability_ Биллинга Маркета - "стабильность",
"жизнеспособность", "устойчивость развития". Ни много, ни мало.

Еще есть другая формулировка. Мы занимаемся задачами общей поддержки Биллинга Маркета:

  - разбором тикетов из поддержки, починкой бизнесовых багов;
  - починкой технических багов;
  - улучшением мониторингов;
  - прочими инфраструктурными доработками.

## Где всё происходит?

У нас есть чат в телеграме, там обсуждаем оперативные вопросы.
Рулит им [Сергей Тесленко](https://staff.yandex-team.ru/teslenko), обращайтесь к нему.

У нас есть [Тикет-зонтик aka Epic](https://st.yandex-team.ru/MARKETBILLING-1314).

У нас есть [Дашборд](https://st.yandex-team.ru/issues/423333).
И есть [просто борд](https://st.yandex-team.ru/agile/board/28854).

У нас есть регулярные встречи
  - [еженедельная по вторникам](https://calendar.yandex-team.ru/event/60813984 "Ретроспектива")
  - [ежедневный синк](https://calendar.yandex-team.ru/event/64890431 "Стендап")

Есть [тикет](https://st.yandex-team.ru/MARKETBILLING-3978), где мы записываем итоги ретроспектив.

И даже есть [Miro-доска](https://miro.com/app/board/uXjVOFRbqs0=/?invite_link_id=665144082330 "Мировая доска"),
если захочется порисовать.

## Саппорт (поддержка)

Один из наиболее важных видов деятельности подразделения састейна - разбор тикетов от специалистов поддержки.

У нас для таких тикетов есть [специальная очередь](https://st.yandex-team.ru/MBSUP/).
Мы договорились, что если в процессе разбора выясняется, что есть баг в Биллинге, или захотелось добавить какой-то
автоматизации (то есть, всегда, когда нужно что-то закоммитить в репозиторий) - то заводим тикет
в очереди MARKETBILLING с компонентой _support_ и прилинковываем к исходному тикету из очереди MBSUP. Если в MBSUP
принесут тикет-близнец существующего, то новый тикет в MARKETBILLING создавать не нужно, а нужно прилинковать к уже
существующему.
