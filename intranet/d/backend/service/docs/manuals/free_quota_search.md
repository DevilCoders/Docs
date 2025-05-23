# Поиск ресурсов в поддереве ABC-сервисов

В этом документе содержится пошаговая инструкция для раздела [Поиск сободных ресурсов](https://abc.yandex-team.ru/free-quota/). Раздел _Поиск свободных ресурсов_ дает возможность оценить общее количество ресурсов поддерева ABC-сервисов и решить задачу поиска конкретного ресурса в поддереве ABC-сервисов.

## Общее количество ресурсов и поиск ресурса

1. Зайдите на <https://abc.yandex-team.ru/> (Каталог сервисов Яндекса)

1. Выберите нужный ABC-сервис

1. Перейдите на вкладку **Квоты** выбранного ABC-сервиса

1. Нажмите на кнопку **Найти свободные ресурсы** для перехода на страницу поиска свободных ресурсов

1. На странице поиска свободных ресурсов укажите ABC-сервис в поле _В каком сервисе искать ресурсы_.

    После выбора отобразится общее количество ресурсов в выбранном ABC-сервисе и всех его потомках.

    Общее количество ресурсов сгруппировано по провайдерам и на этом шаге не учитывает распределение по дата-центрам, сегментам и кластерам. Данные представлены в виде таблицы и показывают количество ресурсов на разных уровнях ресурсной модели:
    - _Всего_ - общее количество ресурса
    - _Баланс_ - количество ресурса на балансе фолдеров
    - _Спущено_ - количество ресурса в аккаунтах провайдера
    - _Аллоцировано_ - количество аллоцированных ресурсов в аккаунтах провайдера
    - _Не аллоцировано_ - количество спущенных, но не аллоцированых ресурсов. Равно разнице между _Спущено_ и _Аллоцировано_
    - _Свободно_ - общее количество неиспользуемых ресурсов, сумма _Баланс_ и _Не аллоцировано_

    Для удобства анализа общего количества ресурсов доступна настрйока отображения столбцов.

    {% note tip %}

    Иконка рядом с полем _В каком сервисе искать ресурсы_ показывает положение выбранного сервиса в дереве ABC-сервисов и позволяет перейти на уровень выше - для увеличения охвата при поиске ресурсов.

    {% endnote %}

1. Выберите провайдера, укажите нужные дата-центры, сегменты и кластеры

    После выбора отобразится общее количество ресурсов с учетом выбранных значений.

1. Укажите тип ресурса

    После выбора типа ресурса отобразится:
    - общее количество этого ресурса в выбранном ABC-сервисе и всех его потомках
    - плоский список ABC-сервисов, в которых есть указанный ресурс

    Список ABC-сервисов также представлен в виде таблицы, но с возможностью сортировки по количеству ресурсов.

## Данные об использовании ресурсов

Данные об использовании рассчитываются только для ресурсов CPU провайдера YP и Strong CPU провайдера YT.

Для YP CPU данные отображаются в виде столбца _Недоиспользовано_ и показывают разницу между фактически использованным количеством квоты и целевым значением аллоцированной квоты за предыдущий день.

Для YT Strong данные отображаются в виде двух значений: _Недоиспользовано_ и _Разброс_. Недоиспользовано равно разнице между фактически использованным количеством и общим количеством квоты ABC-сервиса, среднее за 7 дней. Разброс - отклонение значений потребления квоты от среднего за 7 дней.
