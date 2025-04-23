# [GMA-1576](https://st.yandex-team.ru/GMA-1576) Скрипт для запуска периодической рассылки "Напоминание о созданной РК" + 1 день


### Периодичность сбора:
Каждый день в [основном пайплане](https://nirvana.yandex-team.ru/flow/744f9c71-e96b-4c90-b40d-db16d4fc34ac/96c1d50b-b635-4bf7-b898-31e25fe14082/graph)


### Результаты:
* Таблицы:
  * [sample](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/mailing/GMA-1576/sample) -
  таблица используется для рассылки, перезаписывается каждый день.
  * [log](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/mailing/GMA-1576/log) -
  лог всех таблиц sample, дописывается каждый день.
  В случае перезагрузки в течение дня, останется только последний добавленный sample.
  * [tmp](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/mailing/GMA-1576/tmp) -
  вспомогательная таблица, из которой выбираем необходимые данные для отправки.
* [Граф в Nirvana](https://nirvana.yandex-team.ru/browse?selected=12034309) -
находится в [вспомогательном графе](https://nirvana.yandex-team.ru/browse?selected=11577050)
для рассылок в [основном пайплане](https://nirvana.yandex-team.ru/flow/744f9c71-e96b-4c90-b40d-db16d4fc34ac/96c1d50b-b635-4bf7-b898-31e25fe14082/graph).


**Поля таблицы [sample](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/marketing/smb/micro-dwh/mailing/GMA-1576/sample):**
* **add_date** - дата попадания в лог;
* **add_ts** - дата и время попадания в лог;
* **create_date** - дата пересоздания таблицы;
* **create_date_sha256** - хеш даты пересоздания таблицы;
* **campaign_id** - id РК в бизнесе;
* **balance_client_id** - id балансового клиента;
* **campaign_create_date** - дата создания РК;
* **campaign_type** - тип РК из логов Бизнеса;
* **geoadv_permalink** - id бизнес снапшота;
* **permalink** - id организации из Справочника;
* **company_name** - название организации;
* **rubric_name** - рубрика оргнаизации;
* **email** - email былансовго клиента;
* **email_sha256** - хеш email-а балансового клиента;
* **object_type** - тип организации (сеть/не сеть);
* **object_role** - роль пользователя в организации.


### Порядок сбора данных (указаны названия файлов):
1. **tmp** - забираем РК, которые созданы вчера, но не оплачены
сегодня и дополняем информацией о том, кто её создал и для какой организаци;
2. **log** - исключаем пользователей, для которых не найден email, приоритезируем
РК по количеству дополнительных данных об организации, оставляем уникальную связку
balance_client_id + email (в рамках одного balance_client_id может быть несколько email-ов).
По сути, на этом шаге получаем готовые данные для отправки, но дописываем ими лог.
3. **clearing_log** - очистка лога. На случай, если будет больше одной перезагрузки
данных в день, то в логе сохранится только последний добавленный сэмпл данных.
4. **sample** - формирует таблицу для отправки. Забираем из очищенного лога
данные за текущий день.


### Проблемы


