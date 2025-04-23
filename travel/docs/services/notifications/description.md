---
title: Общее описание
rank: 10
---

### Общее описание системы уведомлений Путешествий

Область применения: уведомления для пользователей через email. В будущем, при необходимости подключения других каналов (tg, viber, etc), они должны появиться в Notifier.

Примеры:

  - PreTrip письма;
  - транзакционные письма;
  - welcome письма;
  - рассылки [Авиа] минимальных цен;
  - дополнительные заказные письма (for ex. с рассрочкой оплаты);

Добавленная ценность: Гомогенные уведомления через переиспользование кода компонент фронтенда. АПИ, позволяющее планировать отправку уведомлений как синхронно (в текущий момент), так и отложенных.


### Политика работы с персональными данными пользователей

#### Хранение
Локации БД:
- SAS
- VLA

Для pretrip-уведомлений в БД сохраняется только email-адрес пользователя. При необходимости будут добавляться другие персональные данные.

#### Логирование
- __Запрещено логировать персональные данные в `stdout/stderr`__ ([RASPTICKETS-20235](https://st.yandex-team.ru/RASPTICKETS-20235))
- Логи в YT с ограниченным доступом:
    - `travel-notifier-testing-pretrip-render-log` ([testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-notifier-testing-pretrip-render-log), [preprod](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-notifier-preproduction-pretrip-render-log), [prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-notifier-production-pretrip-render-log))
