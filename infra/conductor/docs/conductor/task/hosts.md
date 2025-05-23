# Хосты

{% note alert %}

Процедуры, описанные в разделе, доступны только администраторам группы или проекта.

{% endnote %}

{% include [Hosts-HostsBasicInfo](../_includes/concepts/package-props/id-Hosts/HostsBasicInfo.md) %}

Процедуры, выполняемые с хостами:

- [Добавление хоста](#new).
- [Массовое добавление хостов](#massadd).
- [Редактирование хоста](#edit).
- [Удаление хоста](#DeletHost).
- [Групповое удаление хостов](#MassHostDelete).
- [Групповое перемещение хостов в группы](#GroupMoveHosts).

## Добавление хоста {#new}

Для регистрации информации о хосте выполните следующие действия:

1. Откройте окно создания записи о хосте (**Хосты** → **Добавить хост**).

1. Заполните поля:

    #|
    || **Параметр** | **Описание** ||
    || **FQDN** | 
    Полное имя домена, на который может устанавливаться пакет.

    Например: `1run.feeds.yandex.net`. ||
    || **Короткое имя** | Сокращенное имя хоста.

    При автоматическом заполнении (которое выполняется, например, при переходе в другую строку формы) выставляется значение, соответствующее значению поля **FQDN** без доменов второго и верхнего уровней.

    Например, для **FQDN**, имеющего значение `1run.feeds.yandex.net`, поле **Короткое имя** заполняется значением `1run.feeds`. ||
    || **Датацентр** | Название дата-центра, к которому относится хост. Должно соответствовать [одному из определенных](datacenters.md#new) в {{ serviceName }}е значений.

    При вводе значения отображается форма автозаполнения. ||
    || **Группа** | [Группа](groups.md), частью которой должен являться хост. Должна соответствовать [одному из определенных](groups.md#new) в {{ serviceName }}е значений.

    {% include [new-autocomplete](../_includes/task/hosts/id-new/autocomplete.md) %}

    Доступны только те [группы](groups.md), для которых пользователь является администратором группы или [проекта](groups.md#new__project).

    Если в поле введено значение, которое не определено в {{ serviceName }}е, при попытке сохранить данные о хосте необходимо выбрать из списка проект, к которому относится данный хост (см. шаг 4).

    Доступны только [проекты](groups.md#new__project), для которых пользователь определен в качестве администратора. ||
    || **Описание** | Описание хоста в свободной форме. ||
    || **Теги** | Список ключевых слов, характеризующих хост.

    {% include [new-tags-2-sentence](../_includes/task/repos/id-new/tags-2-sentence.md) %}

    {% include [new-task-3-sentence](../_includes/task/repos/id-new/task-3-sentence.md) %} 

    ||
    |#

1. Сохраните изменения (кнопка **Сохранить**). Если в поле **Группа** введено название несуществующей группы хостов, выполните шаги 4-5.

1. Выберите название проекта, к которому относится данный хост (в списочном поле **Проект**).

    {% note alert %}
    
    Доступны только [проекты](groups.md#new__project), для которых пользователь определен в качестве администратора.
    
    {% endnote %}
    
1. Сохраните изменения (кнопка **Сохранить**).

В результате выполнения процедуры в {{ serviceName }}е сохранятся данные о хосте и группе хостов.

## Массовое добавление хостов {#massadd}

Процедура выполняется, если необходимо добавить два и более хостов, имеющих схожую структуру названий.

Для одновременной регистрации информации о нескольких хостах выполните следующие действия:

1. Откройте окно одновременного создания нескольких записей о хостах (**Хосты** → **Добавить много хостов**).

1. Заполните поля:

    #|
    || **Параметр:** | **Описание:** ||
    || **Шаблон FQDN** | Маска для доменов группы хостов.
    
    Соглашения по формату:
    
    - обычным текстом вводятся общие для всех хостов части;
    - в квадратных скобках (`[alt-text]`) через запятую вводятся различающиеся части названия хостов. В скобках можно указать диапазон чисел (например, `[1-15]`).
    
    Например, конструкция `test[01,02].fortesting[03,04].yandex-team.ru` соответствует следующему набору хостов:
    
    - `test01.fortesting03.yandex-team.ru`;
    - `test01.fortesting04.yandex-team.ru`;
    - `test02.fortesting03.yandex-team.ru`;
    - `test02.fortesting04.yandex-team.ru`. ||
    || **Группа** | Группа, частью которой должны быть хосты. Должна соответствовать [одному из определенных](groups.md#new) в {{ serviceName }}е значений.
    
    {% include [new-autocomplete](../_includes/task/hosts/id-new/autocomplete.md) %}
    
    Доступны только те [группы](groups.md), для которых пользователь является администратором группы или [проекта](groups.md#new__project).
    
    Если в поле введено значение, которое не определено в {{ serviceName }}е, то при попытке сохранить данные о хосте необходимо выбрать из списка проект, к которому относится данная группа хостов (см. шаг 3).
    
    Доступны только [проекты](groups.md#new__project), для которых пользователь определен в качестве администратора. ||
    || **Описание** | Описание хостов в свободной форме. ||
    |#

1. Нажмите кнопку **Предпросмотр результата** для анализа списка добавляемых хостов.
    
    Возвращаются:
    
    - форма, аналогичная отображаемой на шаге 2, заполненная заданными значениями;
    - таблица **Предпросмотр результата**, записи в которой содержат данные, описанные в таблице ниже.

    
    #|
    || **Параметр:** | **Описание** ||
    || **FQDN** | {% include [new-fqdn-first-sentence](../_includes/task/hosts/id-new/fqdn-first-sentence.md) %} ||
    || **Короткое имя** | {% include [new-short-name-desc](../_includes/task/hosts/id-new/short-name-desc.md) %}
    
    Генерируется автоматически. Короткие названия должны быть определены и уникальны. ||
    || **Датацентр** | Название дата-центра, к которому относится хост.
    
    В форме группового добавления данных о хостах названия дата-центров не задаются и для их определения необходимо выполнить процедуру [Редактирование хоста](#edit). ||
    || **Группа** | [Группа](groups.md), частью которой должен являться хост. ||
    || **Описание** | {% include [new-description-shortdesc](../_includes/task/hosts/id-new/description-shortdesc.md) %} ||
    || **Ошибки и предупреждения** | Сообщения об ошибках и предупреждениях, возникших при формировании предварительного списка записей о хостах.
    
    Некоторые возможные значения:
    
    - <q>Датацентр не найден</q> — информация о дата-центре не зарегистрирована в {{ serviceName }}е. Запись выделена желтым цветом. При массовом добавлении данных о хостах дата-центры не задаются, поэтому ошибка не является критичной и может быть проигнорирована;
    - <q>Short name не может быть пустым</q> и/или <q>Short name имеет неверное значение</q> — невозможно определить короткое имя хоста. Запись выделена красным цветом. Для исправления необходимо переопределить маску для доменов группы хостов;
    - <q>Short name уже существует</q> — короткое название хоста не является уникальным. Запись выделена красным цветом. Для исправления необходимо переопределить маску для доменов группы хостов;
    - <q>Fqdn уже существует</q> — FQDN хоста, формируемый в результате обработки структуры, заданной в поле **Шаблон FQDN**, уже определен в {{ serviceName }}е и не может быть использован. Запись выделена красным цветом. Для исправления необходимо переопределить маску для доменов группы хостов. ||
    |#

    Если на шаге 2 в поле **Группа** введено название несуществующей группы хостов, необходимо определить проект, к которому относится данная группа (в списочном поле **Проект для группы**).

    {% include [new-project-restriction](../_includes/task/hosts/id-new/project-restriction.md) %}

    В случае ошибок (записей, выделенных красным цветом) переопределите параметры (повторно выполните шаги, начиная с 2. В противном случае будут сохранены записи только о тех хостах, которые не являются ошибочными.

1. Сохраните изменения (кнопка **Сохранить**).

Для определения дата-центров, к которым относятся созданные хосты, задайте значение поля **Датацентр** согласно описанию процедуры [Редактирование хоста](#edit).

## Редактирование хоста {#edit}

Для редактирования информации о хосте выполните следующие действия:

1. Откройте список доступных хостов (**Хосты**).
1. Выберите хост из списка. Для ограничения списка отображаемых хостов используйте строку поиска.
1. Внесите изменения в поля формы (см. шаг 2 процедуры [Добавление хоста](#new)).
1. Сохраните изменения (кнопка **Сохранить**).

## Удаление хоста {#DeletHost}

Для удаления информации о хосте выполните следующие действия:

1. Откройте список доступных хостов (**Хосты**).
1. Выберите хост из списка. Для ограничения списка отображаемых хостов используйте строку поиска.
1. Нажмите кнопку **Удалить**.
1. Подтвердите намерение удалить информацию о хосте (кнопка **OK**).

В результате выполнения процедуры данные о хосте удаляются из {{ serviceName }}а.

## Групповое удаление хостов {#MassHostDelete}

Для удаления двух и более (в общем случае — одной и более) записей о хостах выполните следующие действия:

1. Откройте список доступных хостов (**Хосты**).
1. Заполните поля выбора, соответствующие удаляемым хостам.
1. Выберите значение <q>Удалить</q> в списочном поле под списком доступных хостов.
1. Нажмите кнопку **Ok** для удаления данных о выбранных хостах.
1. Подтвердите намерение удалить информацию о хостах (кнопка **Удалить**).

## Групповое перемещение хостов в группы {#GroupMoveHosts}

{% note alert %}

Хосты могут быть перемещены только в те [группы](groups.md), для которых пользователь является администратором группы или [проекта](groups.md#new__project).

{% endnote %}

Для группового перемещения хостов в [группы](groups.md) выполните следующие действия:

1. Откройте список доступных хостов (**Хосты**).
1. Заполните поля выбора перемещаемых хостов.
1. Выберите значение <q>Переместить в группу</q> в списочном поле под списком доступных хостов.
1. Начните вводить название группы, в которую необходимую переместить записи о хосте. Используйте подсказку автозаполнения для выбора требуемого значения.
1. Нажмите кнопку **Ok**.
1. Подтвердите намерение переместить хосты в группу (кнопка **Сохранить**).
