# Сервисы

{% include [macroses-musician-restriction](../_includes/task/macroses/id-macroses/musician-restriction.md) %}

{% include [Services-ServicesBasicInfo](../_includes/concepts/package-props/id-Services/ServicesBasicInfo.md) %}

Сервисы, для которых должны выполняться действия при выкладке, определяются в [свойствах пакета](packages.md#PackageAddSt2)

Процедуры, выполняемые с сервисами:

- [Добавление сервиса](#new).
- [Редактирование сервиса](#edit).
- [Удаление информации о действиях с сервисом](#DeleteService).

## Добавление сервиса {#new}

Для регистрации информации о действиях с сервисом выполните следующие действия:

1. Откройте окно создания записи о сервисе (**Сервисы** → **Добавить сервис**).
    
1. Заполните поля формы:
    
    #|
    || **Параметр** | **Описание** ||
    || **Имя** | Название действия с сервисом. ||
    || **Описание** | Описание скрипта в свободной форме. ||
    || **Скрипт** | Скрипт, выполняемый при выкладке пакета. В зависимости от [свойств пакета](packages.md) может быть вызван до или после выкладки.
    
    Если в поле не указан скрипт, то действия зависят от автоматизации выкладки:
    
    - при выкладке автоадмином выполняется команда `/etc/init.d/<Название сервиса> restart`;
    - при выкладке администратором тип действия с сервисом может быть задан вручную: `/etc/init.d/<Название сервиса> {start / stop / restart}`.
    
    {% note info %}
    
    Если в поле задан пробел, то {{ serviceName }} обрабатывает значение, как заполненное, т.е. указанная выше команда не выполняется.
    
    {% endnote %}
    
    Для выполнения другой команды необходимо задать скрипт в данном поле. Принятая к исполнению команда задается с помощью комбинации символов `##`, например: 
    
    `/etc/init.d/AUTO ## auto-mailer`.
    
    Чтобы подставить в скрипт название пакета, при выкладке которого был запущен сервис, используйте команду `#package#`. При выполнении скрипта `#package#` будет заменен на имя пакета с учетом версионирования.
    
    В скрипте может использоваться `sudo`. Условия применения: Если требуется использовать `sudo` всеми командами строки, то команда должна быть помещена в начале строки. Если требуется использовать `sudo` строго в определенных местах скрипта, то необходимо использовать команду `#sudo#`:
    
    - В начале строки — права суперпользователя распространяются на весь скрипт.
    - В определенных местах — права суперпользователя распространяются строго на указанные команды, например:
    
    `if test -e /etc/init.d/apache2; then #sudo# /etc/init.d/apache2 ## fi`
    
    Если права пользователя `root` для выполнения команды не требуются, команда `sudo` игнорируется. ||
    || **Настройки запуска** | Задержка перезапуска сервисов на разных хостах до/после выкладки пакета.
    
    Возможные значения:
    
    - <q>параллельно</q> — параллельный перезапуск на разных хостах;
    - <q>последовательно с задержкой</q> — последовательный перезапуск на разных хостах с задержкой (в секундах), указанной в поле **сек.**. ||
    || **Теги** | Список ключевых слов, характеризующих сервис.
    
    {% include [new-tags-2-sentence](../_includes/task/repos/id-new/tags-2-sentence.md) %}
    
    {% include [new-task-3-sentence](../_includes/task/repos/id-new/task-3-sentence.md) %} ||
    |#
    
1. Сохраните изменения (кнопка **Сохранить**).

В результате в {{ serviceName }}е регистрируется информация о сервисе. Он может быть назначен пакету при [добавлении](packages.md#new).

## Редактирование сервиса {#edit}

Для редактирования информации о действиях с сервисом выполните следующие действия:

1. Откройте список доступных сервисов (**Сервисы**).
1. Выберите сервис из списка. Для ограничения списка отображаемых сервисов используйте строку поиска.
1. Внесите изменения в поля формы (см. шаг 2 процедуры [Добавление сервиса](#new)).
1. Сохраните изменения (кнопка **Сохранить**).

## Удаление информации о действиях с сервисом {#DeleteService}

Для удаления информации о действии с сервисом выполните следующие действия:

1. Откройте список доступных сервисов (**Сервисы**).
1. Выберите сервис из списка. Для ограничения списка отображаемых сервисов используйте строку поиска.
1. Нажмите кнопку **Удалить**.
1. Подтвердите намерение удалить информацию о сервисе (кнопка **OK**).

В результате выполнения процедуры данные о действиях с сервисом удаляются из {{ serviceName }}.
