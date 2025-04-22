Более полная документация по счётчикам на wiki: https://wiki.yandex-team.ru/search-interfaces/multimedia/counters/

# Счётчики в Видео
[Инструкция для React](video-viewer/src/lib/Counters/README.md)

Старая документация на Вики: https://beta.wiki.yandex-team.ru/search-interfaces/multimedia/video/counters/islands/.

## Stred-счётчики
Полный список зарегистрированных stred-счётчиков Видео находится здесь: https://stat.yandex-team.ru/Counters/Video.
Вызывается через метод `data.stat.cpCounter`. В этом случае при клике по элементу просто вызывается метод `cp`, который отправляет в фоне ajax- (или другой) запрос. Метод может вызываться либо явно из js-кода, либо через атрибут data-counter (чаще всего для блока link).

Далее приведен список stred-счётчиков, которые используются в Видео.
**NB:** полная актуальность списка не гарантируется, более надёжным способом остаётся grep по коду (`ag 'cpCounter' -w -G '\.priv'` в привах и что-нибудь вроде `ag 'cp\(' -G video` в клиентском js).
