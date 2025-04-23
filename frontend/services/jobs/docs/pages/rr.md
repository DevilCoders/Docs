# Раскатка в Report Renderer

1. Отвести релиз можно через кнопку `Run release`, перейдя по [ссылке](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fjobs&id=release). В списке тикетов, попадающих в релиз отображаются только те, которые затронули код `frontend/services/jobs`. Тикеты с правками в `frontend/services/turbo` пока здесь не отображаются (WIP).
2. Найти релизный тикет можно по [ссылке](https://st.yandex-team.ru/issues/?_q=Queue%3ASEAREL+AND+Summary%3A%22frontend%40jobs%22). Тикет назначается на текущего дежурного по фронтенду.
3. При появлении комментария TO TESTERS релиз должен выкатиться на [приемку](https://rctemplates-jobs.hamster.yandex.ru/jobs) и там его можно проверить. Ссылку на приемку внутри тикета игнорируем. Стоит иметь в виду, что база тестовая.
4. Переводим релизный тикет через статусы **In progress** → **Теsted** → **Ready for prod** — теперь ждём сообщения робота: "Зарелизили таск <task_id> с пакетом шаблонов".
5. Следуем [инструкции](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/selfduty/#relizyvsharediydo). Нюансы:

a) Мы живем НЕ в SHARED, [наш дашбоард](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report-renderer-jobs/)
b) [Наши мониторинги](https://yasm.yandex-team.ru/panel/koreil._6Uh7Mg/)
c) Нам не нужно брать лок
d) В пункте 5 ("Выбираем в столбце справа релиз нужного сервиса") нам нужен [вот этот кусочек](https://jing.yandex-team.ru/files/olgakozlova/2021-03-17T10%3A04%3A14Z.png)
e) Возможна ошибка, что в diff будут присутствовать [лишние id](https://nda.ya.ru/t/ZO7GXGns4DrAHf). [Как поступать в этом случае](https://st.yandex-team.ru/INFRADUTY-18401#61389ae7622d88436c70e755). Пункт неактуален после закрытия [SWAT-7685](https://st.yandex-team.ru/SWAT-7685)
