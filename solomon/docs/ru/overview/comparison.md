# Отличия от известных систем мониторинга

## Отличия от модели данных Graphite {#solomon-vs-graphite}

В системе мониторинга Graphite каждая метрика идентифицируется набором меток, как и в Solomon. Однако меткой в Graphite является одна строка, а не пара строк, в отличие от Solomon. Метки в Graphite разделены точками. Пример идентификатора метрики в Graphite: `media.afisha.combine.admin01d_afisha_tst_yandex_net.nginx.common.status.200`.

Метрики в Graphite организованы в древовидную структуру, в которой на каждом уровне дерева отображаются значения меток. Модель данных Solomon является более гибкой, так как позволяет описать произвольное пространство метрик, а не только иерархическое.

![Навигация по метрикам в Graphite](_assets/graphite.png "Навигация по метрикам в Graphite"){ width="1552" }
<small>Рисунок 1 — Навигация по метрикам в Graphite.</small>
