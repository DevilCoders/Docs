# [OKOREPORTS-5063](https://st.yandex-team.ru/OKOREPORTS-5063) Таблица для отправки опросов в Whatsapp по сегменту "2 Не купили (ТМ)"

### Описание:
Для сегмента "2 Не купили (ТМ)" (только AMO) производится повторная отправка
анкет в Whatsapp. Для отправки анкет в Whatsapp собирается выборка
из тех лидов, которым были отправлены опросы на электронную почту.
Критерии для формирования выборки:
- не начали заполнять анкету в течение трёх дней, от даты отправки письма;
- есть тег Whatsapp 2.

Процесс сборки таблиц находится в пайплайне: **[other_processes](https://nirvana.yandex-team.ru/flow/42f41a66-8387-49e0-aa7c-b2af7d45a9cb/a9861de1-ecb0-41d2-8791-5996b732111d/graph)**,
который запускается в [основном пайплайне](https://nirvana.yandex-team.ru/flow/99090e6d-537b-4284-a4b4-043b6751b7a0/46a5daef-e184-40af-9af7-2248f16eab4b/graph)
новой версии Дшёвого Трекинга.


### [Nirvana](https://nirvana.yandex-team.ru/flow/42f41a66-8387-49e0-aa7c-b2af7d45a9cb/4a7b9172-7f8f-4085-8521-2e73f6b0968f/graph/FlowchartBlockOperation/code/svn_checkout_deterministic_2)


### Таблицы:
- **[sample](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/cheap-monitoring/other_processes/whatsapp_segment_2/sample)** -
ежедневно обновляется, именно её нужно использовать для отправки.
  - **_create_dt** - дата создания таблицы (будет равна дате отправки);
  - **_create_ts** - дата и время создания таблицы;
  - **email_sha256** - хеш email-а (добавлен в ссылку);
  - **lead_id** - id лида из AMO CRM;
  - **org_name** - название организации (если сеть, то сети);
  - **personal_link** - персональная ссылка на опрос (добавлен хеш email-а);
  - **personal_short_link** - сокращённая персональная ссылка;
  - **segment_id** - идентификатор сегмента "Дешёвого трекинга".


- **[log](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/cheap-monitoring/other_processes/whatsapp_segment_2/log)** -
хранит данные о семплах, каждый день добавляется новый семпл. Предусмотрено
удаление дубликатов на случай повторных перезагрузок в рамках одного дня.
  - поля аналогичны "sample"
  - **_add_dt** - равно *_create_dt* из "sample";
  - **_add_ts** - равно *_create_ts* из "sample";
  - **_log_update_dt** - дата обновления лога;
  - **_log_update_ts** - дата и время обновления лога.


- Остальные таблицы являются вспомогательными.

### Порядок сбора (названия файлов равны названиям таблиц):
1. **prepare** - собираем данные по криетриям;
2. **prepare_short_links** - сокращаем ссылки;
3. **sample** - собираем данные для сегодняшней отправки;
4. **log** - сохраняем в лог сегодняшнюю таблицу.
