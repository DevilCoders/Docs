## 30-секундные хартбиты

Скрипт отправки 30-секундных хартбитов.
Как это работает:
1. Инлайнится скрипт `b-page__js_sb-heartbeats.inline.js`
2. Устанавливаются параметры счётчиков (одинаковые для всех роликов):
    ```js
    window.Ya.Video.hb.setCounterParams({
        period: 30, // Время в секундах, с какой периодичностью отправлять хартбиты
        dtype: 'stred', // Всегда stred
        pid: 197, // тачи 565, десктопы 197
        cid: 72339, // всегда 72339
        path: 'test.heartbeat' // путь счётчика
    });
    ```
3. Устанавливаются параметры ролика (для каждого ролика свои) нужно обновлять при нон-стопе, кликах в релейтеды/выдачу — при загрузке ролика в видео-плеер:
    ```js
    window.Ya.Video.hb.setVideo({
        reqid: data.reqdata.reqid, // reqid текущего ролика (с выдачи или релейтеда)
        click_id: (new Date()).getTime(), // насколько я понял, время перехода к новому ролику
        select_event: 'url', // non-stop | click (открыт пользователем) | default (автовыделенное видео) | url (открытие ролика по урлу)
        duration: selected.duration, // продолжительность ролика
        jsapi: BEMPRIV.block('player2').isPlayerEventsSupported(selected.PlayerId), // поддержка jsapi
        url: selected.url // урл ролика
    });
    ```
