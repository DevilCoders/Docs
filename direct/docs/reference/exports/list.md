# YT-Выгрузки Директа и их потребители

## Шаблон описания { #template }

- **выгружаемая таблица/каталог:**
   - xxx
- **тикет в котором заказывали:**
   - [NNNN-000: тикет](https://st.yandex-team.ru/NNNN-000)
- **кластер на который заказывали:**
   - xxx
- **ABC-сервис заказчика, один-два контакта заказчика:**
   - xxx (ссылки на abc, staff)
- **как часто нужна выгрузка (какую гарантию просили / какую обещаем):**
   - xxx

## Счётчики из кампаний для Метрики { #counters-from-campaigns-for-metrica }

- **выгружаемая таблица/каталог:**  
   - [//home/direct/db/campaigns](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/campaigns)
   - [//home/direct/db/clients](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/clients)
   - [//home/direct/db/users](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/users)
- **тикет в котором заказывали:**  
   - [METR-42366: сделать нормальный DirectClientIdTaskMisc](https://st.yandex-team.ru/METR-42366#604a5398a136d40bda1d4681)
- **кластер на который заказывали:**  
   - Hahn
   - Arnold
- **ABC-сервис заказчика, один-два контакта заказчика:**  
   - [Метрика](https://abc.yandex-team.ru/services/conv/)
   - [Александр Башкин](https://staff.yandex-team.ru/albashkin)
- **как часто нужна выгрузка (какую гарантию просили / какую обещаем):**  
   - раз в сутки

## Типы целей Метрики для статистики БК { #metrika-goal-types-for-bs }

- **выгружаемая таблица/каталог:**
    - [//home/direct/mysql-sync/current/ppcdict/straight/metrika_goals](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/mysql-sync/current/ppcdict/straight/metrika_goals)
- **тикет в котором заказывали:**
    - [DIRECT-151840: Добавить справочник типы целей](https://st.yandex-team.ru/DIRECT-151840#6138a6e8608a232d0a0b6f61)
- **кластер на который заказывали:**
    - Hahn
    - Arnold
- **ABC-сервис заказчика, один-два контакта заказчика:**
    - [Эксплуатация статистики БК](https://abc.yandex-team.ru/services/yabsstatistic/)
    - [Тимур Власов](https://staff.yandex-team.ru/zasalamel)
- **как часто нужна выгрузка (какую гарантию просили / какую обещаем):**
    - нужны более актуальные данные, чем в [//home/direct/db/metrika_goals](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/metrika_goals), которые готовятся раз в сутки
    - обещаем не удалять колонки goal_id и goal_type без предупреждения
