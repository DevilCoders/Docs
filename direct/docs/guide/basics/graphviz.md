# Graphviz
Graphviz — пакет утилит для автоматической визуализации графов, заданных в виде описания на языке DOT.  
С их помощью удобно рисовать всякие схемы со стрелочками.

Примеры ищите по ссылкам и в интернете, а эта инструкция расскажет о том, где и как использовать такие графики.

## Вики/трекер
Наш викиформаттер [поддерживает](https://wiki.yandex-team.ru/wiki/vodstvo/formatters/graphviz/) Graphviz.
Графы можно описывать как разметку кода `%% ... %%` с указанием синтаксиса `(graphviz dot)` и использовать их на вики и в трекере.

Для примера (со страницы [{#T}](../../concepts/dev/ticket-workflow.md)), код:

{% code '/direct/docs/concepts/dev/ticket-workflow.dot' %}

при вставке в трекер или на вики превращается вот в такую картинку:

![sample](../../concepts/dev/_assets/ticket-workflow-simplified.svg "Визуализация графа")

## Генерация из файла
В нашей документации есть схемы, как раз записанные в виде dot-файлов.

Платформа документации пока не умеет прозрачно превращать их в картинки (лайки ставить [сюда](https://st.yandex-team.ru/DOCSTOOLS-143)),
поэтому конвертировать описания графов нужно вручную.
Для этого нужен установленный graphviz (под MacOS: `brew install graphviz`).

Картинка из примеры выше получилась запуском (из корня документации) вот такой команды:
```sh
dot concepts/dev/ticket-workflow.dot -Tsvg -o concepts/dev/_assets/ticket-workflow-simplified.svg
```

## Ссылки
- [сайт с документацией](https://www.graphviz.org/documentation/)
   - [формы узлов](https://www.graphviz.org/doc/info/shapes.html)
   - [формы стрелок](https://www.graphviz.org/doc/info/arrows.html)
   - [цветовая палитра](https://graphviz.org/doc/info/colors.html)
   - [все аттриубты](https://graphviz.org/doc/info/attrs.html)
- вики-страница с [примерами dot-синтаксиса](http://lib.custis.ru/Graphviz)
