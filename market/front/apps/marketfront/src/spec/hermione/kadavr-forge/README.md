# kadavr forge

Немного автоматизирует процесс установки стейта и получения нужного ответа от кадавра.

1. Выполняет запрос в бэк, сохраняет ответ
2. Устанавливает стейт в кадавр
3. Выполняет запрос в кадавр, сохраняет ответ
4. При изменении скрипта установки стейта, перезапускает запрос в кадавр и сохраняет ответ
5. Может выдавать diff, но сохраняет все в файлах, можно смотреть в IDE

## Зачем?

Для получения нужного состояния страницы в автотесте нужно чтобы довольно много запросов  ответили определенным образом.
Скрипт немного упрощает ручную работу по получению и сравнению нужных ответов.


## Usage

- Создать скрипты requests/first.sh, second.sh
- создать config.js по config.example
- запустить ./forge.js
