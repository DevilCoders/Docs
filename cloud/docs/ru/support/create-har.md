# Сохранение взаимодействия браузера и сервера в HAR-файл

Если при работе в консоли {{ yandex-cloud }} возникла ошибка, разобраться с ней поможет HAR-файл. Это сетевой журнал взаимодействий браузера с веб-страницей. Чтобы специалисты {{ yandex-cloud }} обнаружили причину некорректной работы сервиса, включите запись журнала и воспроизведите ошибку. Сохраните HAR-файл и передайте его в [техническую поддержку]({{ link-console-support }}).

{% list tabs %}

{% if product == "yandex-cloud" %}

- Яндекс Браузер

  {% include [create-har-yandex](../_includes/support/create-har-yandex.md) %}

{% endif %}

- Google Chrome

  1. На странице с ошибкой нажмите сочетание клавиш **Ctrl** + **Shift** + **J** (**⌥** + **⌘** + **J** для macOS) или откройте меню ![image](../_assets/vertical-ellipsis.svg) → **Дополнительные инструменты** → **Инструменты разработчика**.
  1. Перейдите на вкладку **Network**.
  1. Убедитесь, что запись сетевого журнала включена: в левом верхнем углу кнопка красная ![image](../_assets/support/chromium-log-record.png =20x20). Если кнопка черная, нажмите ее.
  1. Включите опцию **Preserve log**.
  1. Чтобы в HAR-файле оказались только записи, касающиеся ошибки, очистите журнал: нажмите ![image](../_assets/support/chromium-log-clear.png =20x20) справа от кнопки записи сетевого журнала.
  1. Обновите страницу или повторите действия, которые приводят к ошибке.
  1. Правой кнопкой мыши нажмите на таблицу и выберите **Save all as HAR with content**.
  1. Приложите HAR-файл к сообщению в [техническую поддержку]({{ link-console-support }}).

- Opera

  1. На странице с ошибкой нажмите сочетание клавиш **Ctrl** + **Shift** + **J** (**⌥** + **⌘** + **J** для macOS) или откройте меню **Opera** → **Разработка** → **Инструменты разработчика**.
  1. Перейдите на вкладку **Network**.
  1. Убедитесь, что запись сетевого журнала включена: в левом верхнем углу кнопка красная ![image](../_assets/support/chromium-log-record.png =20x20). Если кнопка черная, нажмите ее.
  1. Включите опцию **Preserve log**.
  1. Чтобы в HAR-файле оказались только записи, касающиеся ошибки, очистите журнал: нажмите ![image](../_assets/support/chromium-log-clear.png =20x20) справа от кнопки записи сетевого журнала.
  1. Обновите страницу или повторите действия, которые приводят к ошибке.
  1. Правой кнопкой мыши нажмите на таблицу и выберите **Save all as HAR with content**.
  1. Приложите HAR-файл к сообщению в [техническую поддержку]({{ link-console-support }}).

- Mozilla Firefox

  1. На странице с ошибкой нажмите сочетание клавиш **Ctrl** + **Shift** + **C** (**⌥** + **⌘** + **C** для macOS) или откройте меню ![image](../_assets/support/firefox-menu.png) → **Другие инструменты** → **Инструменты веб-разработчика**.
  1. Перейдите на вкладку **Network**.
  1. Обновите страницу или повторите действия, которые приводят к ошибке.
  1. Нажмите на таблицу правой кнопкой мыши и выберите **Save all as HAR**.
  1. Приложите HAR-файл к сообщению в [техническую поддержку]({{ link-console-support }}).

- Microsoft Edge

  1. На странице с ошибкой нажмите сочетание клавиш **Ctrl** + **Shift** + **J** (**⌥** + **⌘** + **J** для macOS) или откройте меню ![image](../_assets/horizontal-ellipsis.svg) → **Другие инструменты** → **Средства разработчика**.
  1. Перейдите на вкладку **Network**.
  1. Убедитесь, что запись сетевого журнала включена: в левом верхнем углу кнопка красная ![image](../_assets/support/edge-log-record.png =20x20). Если кнопка черная, нажмите ее.
  1. Включите опцию **Preserve log**.
  1. Чтобы в HAR-файле оказались только записи, касающиеся ошибки, очистите журнал: нажмите ![image](../_assets/support/edge-log-clear.png =20x20) справа от кнопки записи сетевого журнала.
  1. Обновите страницу или повторите действия, которые приводят к ошибке.
  1. Нажмите на таблицу правой кнопкой мыши и выберите **Save all as HAR with content**.
  1. Приложите HAR-файл к сообщению в [техническую поддержку]({{ link-console-support }}).

- Safari

  1. На странице с ошибкой откройте меню **Safari** → **Настройки** → **Дополнения** и включите опцию **Показывать меню «Разработка» в строке меню**.
  1. В меню **Разработка** выберите **Показать веб-инспектор** или используйте сочетание клавиш **⌥** + **⌘** + **J**.
  1. Перейдите на вкладку **Сеть**.
  1. Включите опцию **Сохранить журнал**.
  1. Обновите страницу или повторите действия, которые приводят к ошибке.
  1. В правом верхнем углу вкладки нажмите кнопку **Экспортировать**.
  1. Приложите HAR-файл к сообщению в [техническую поддержку]({{ link-console-support }}).

{% if product == "cloud-il" %}

- Яндекс Браузер

  {% include [create-har-yandex](../_includes/support/create-har-yandex.md) %}

{% endif %}

{% endlist %}
