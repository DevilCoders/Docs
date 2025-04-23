## RecommendationsApplyJob

### Продукт/подсистема

Рекомендации для пользователей в веб-интерфейсе.


### Роль в работе продукта/подсистемы

Асинхронное применение рекомендаций (если их больше 30), при нажатии пользователем "Применить".


### Датафлоу

- Выполняется раз в 5 минут.
- Читает по 10 рекомендаций, которые нужно применить, из таблицы [recommendations_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/recommendations_queue.html).
- Пишет в эту же таблицу, что эти рекомендации выполняются текущим воркером (поле `recommendations_queue.par_id`).
- В таблице `recommendations_status` по ид рекомендации ставит статус `in_progress`.
- Применяет рекомендацию.
- В таблице `recommendations_status` по ид рекомендации ставит статус `done` или `failed`.
- Удаляет запись из таблицы `recommendations_queue`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.RecommendationsApplyJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'recommendations.RecommendationsApplyJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будут применяться все рекомендации — критично.
После восстановления рекомендации применятся.


### Как пользователи (или команда) заметят проблему и через какое время

При нажатии кнопки "Применить" ничего не произойдет и через день может появиться повторная рекомендация.


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Ирин](https://staff.yandex-team.ru/snirinn), [Игорь Костромин](https://staff.yandex-team.ru/elwood), [Алексей Кашицын](https://staff.yandex-team.ru/aliho)


### Желательное время исправления в случае поломки

В течение нескольких часов.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
