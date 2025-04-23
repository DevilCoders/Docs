## Запуск скрипта html_to_pdf

На компьютере должен быть установлен Docker

Затем в директории `cargo-outsource` исполняем следующую команду, для того,
 чтобы собрать образ:
```shell script
docker build . -t script
```

Запускаем скрипт командой, указанной ниже. При этом последним аргументом идёт
 относительный путь до вашей верстки в директории `cargo-outsource`.

```shell script
docker run -it -v ${PWD}:/project script python3 scripts/html_to_pdf.py --html_filepath {ПУТЬ ДО ВЕРСТКИ}
```
Например, если ваша верстка лежит по пути `cargo-outsource/invoice.html`,
 то команда будет выглядеть так:
```shell script
docker run -it -v ${PWD}:/project script python3 scripts/html_to_pdf.py --html_filepath invoice.html
```