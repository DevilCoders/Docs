# schedule_feedback_worker

Вызывается по [крону](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_feedback/src/schedule_feedback_worker/cfg/cron.conf).
[Краткое описание на wiki](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/wikinktasks_cur/#ktochemzanimaetsja).

## Выполняет несколько задач

### Schedule

Только что созданная фидбэчина не видна в НК.
Сначала её должен обработать этот шедулер.

Шедулер вычисляет и сохраняет список AOI для позиции фидбэчины.
И делает Reveal, что делает фидбэк видимым в НК.

Дополнительно шедулер умеет:
 * автоматически реджектить и апрувить фидбэк
 * отложить фидбэк в отдельную корзину Deferred
 * [объединить новый фидбэк с дубликатами](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/wikinktaskscur/#dublisozdaniedublejjotkljucheno) из корзины Deferred \[отключено\]

### Release overdue

Пользователь в карточке фидбэка в НК нажимает "Взять". И фидбэк лочится на него.
Эта задача снимает такие локи взятые больше часа назад.

### Reject overdue

Реджектит фидбэк отправленный в need-info больше месяца назад.

### Премодерация фидбека

Для фидбека от пользователей (источник `fbapi`) сделана премодерация фотографий: если в фидбеке есть неприемлемый контент, то фидбек автоматически отклоняется с причиной `spam`. Отклоняется до того, как фидбек становится виден в фидах/пинах НК, при этом фидбек доступен по прямой ссылке.
Технически премодерация реализована через [Чистый веб](https://wiki.yandex-team.ru/jandekspoisk/antispam/cleanweb/), [тикет](https://st.yandex-team.ru/CLEANWEB-2130), [исходники](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_feedback/src/schedule_feedback_worker/lib/fbapi/traits.cpp?rev=r9286367#L85). При анализе фотографий по одной отправляем их по http в чистый веб, если хотя бы под одной фотографии получили плохой вердикт, то считаем весь фидбек неприемлемым.
