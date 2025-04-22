# История версий

## 0.3.4-beta.1 от 30.06.2022

- [fix]: `deps`: Технический релиз, стабилизация зависимостей

## 0.3.3 от 28.06.2022

- [feat]: `modals`: Улучшение в ModalLayout. Избавление от альтернатив.

## 0.3.2 от 23.06.2022

- [feat]: `forms2`: Множество мелких улучшений в контейнерах

## 0.3.1 от 23.06.2022

- [fix]: `all`: Восстановлены изменения между 0.2.9 и 0.3.0, которые почему-то пропали из репы

## 0.3.0 от 25.05.2022

-  [feat]: `forms2`: Контейнеры для форм (множество улучшений)
-  [feat]: `all`: Обновление common до 10 версии (ломающее, требует каскадного обновления в проекте)

## 0.2.9 от 31.03.2022

-  [feat]: `forms2`: Контейнеры для форм
-  [feat]: `forms2`: Несколько новых компонентов для форм
-  [feat]: `forms2`: Мелкие улучшения в модуле форм

## 0.2.7 от 02.03.2022

-  [feat]: `suggestions`: Возможность подписаться на ошибки при загрузке данных для саджеста: `SuggestSelect.onError`

## 0.2.6 от 01.02.2022

-  [fix]: `small_components`: Поддержка дефисов в названиях ABC сервисов. Также обновлён список scopes ABC.

## 0.2.5-beta.1 от 28.12.2021

-  [feat]: `formatters`: Новые форматтеры: `camelCase`, `pascalCase`, `deCapitalize`, `splitToWords`
-  [feat]: `helpers`: Хелпер для фильтрации ошибок внутри `catch` - `isOneOfErrors`
-  [feat]: `small_components`: Новые компонент `Skeleton`

## 0.2.3,0.2.4 от 24.12.2021

-  Технические релизы, улучшен результат сборки (выкручиваюсь, пока не внедрил сборку в ES модули)

## 0.2.2 от 21.12.2021

-  [fix]: `small_components`: Для Pagination не показывается номер последней страницы, если страница только одна.
-  [feat]: `small_components`: Опция Pagination.hideSinglePage, чтобы не показывать пагинацию для одной страницы

## 0.2.1 от 01.11.2021

-  [fix]: `small_components`: Для Pagination исправлено переключение числа элементов на странице
-  [fix]: `small_components`: Для ButtonLink в случае локальной ссылки теперь прокидывается className

## 0.2.0 от 28.10.2021

-  [feat]: `all`: Из библиотеки удалена поддержка lego-on-react и все виды его использования.

## 0.1.40 от 16.09.2021

-  [feat]: `libs`: Обновлен пакет `data-ui/common`. Добавлены костыли для поддержки `lego-on-react`, пока его не
   выпилили.

## 0.1.39 от 09.09.2021

-  [fix]: `small_components`: Для подсказок внутри label теперь блокируется всплытие события клика
-  [feat]: `layout`: Возможность подписаться на ошибку при показе `ErrorBoundary`

## 0.1.38 от 24.08.2021

-  [fix]: `forms2`: Верстка "муравьев" в ридонли режиме

## 0.1.37 от 16.08.2021

-  [fix]: `forms2`: Запрет изменения значений в `input[type=number]` при скролле (доработка версии 0.1.36)
-  [feat]: `all`: Включение исходников в пакет (справочно)

## 0.1.36 от 31.07.2021

-  [fix]: `forms2`: Запрет изменения значений в `input[type=number]` при скролле

## 0.1.34 от 11.06.2021

-  [feat]: `http`: Поддержка pre-request hooks

## 0.1.33 от 04.06.2021

-  [feat]: `small_components`: Доработки в `UserName`: синяя буква для групп, возможность отключить аватар и передать
   свое имя

## 0.1.31 от 14.05.2021

-  [feat]: `formatters`: Поддержка сериализации BigInt в `json`

## 0.1.30 от 27.04.2021

-  [feat]: `layout`: Новый модуль с компонентами `EmptyContainer`, `ErrorBoundary`, `SwitchRoutes`
-  [fix]: `all`: Доработки в области интеграции с новыми модальными окнами

## 0.1.28 от 09.04.2021

-  [feat]: `modals`: Фикс `ModalLayout.disabled`

## 0.1.27 от 01.04.2021

-  [fix]: `forms2`: `hideErrors` теперь убирает и красную подсветку
-  [feat]: `forms2`: Мелкий фикс верстки для `bigLabel`
-  [feat]: `modals`: Используется `Dialog` вместо `LegoModal`
-  [feat]: `small_components`: Используется `HelpTooltip` из data-ui/common внутри `Hint`
-  [feat]: `utils`: Удалён `fixedMemo`

## 0.1.26 от 22.03.2021

-  [feat]: `forms2`: Мелкий фикс верстки для `bigLabel`

## 0.1.25 от 19.03.2021

-  [feat]: `forms2`: Поддержка свойств `bigLabel` и `readonlyDots` для `FieldLayout`

## 0.1.24 от 18.03.2021

-  [feat]: `small_components`: Добавлены компоненты `SmartTabs` и `SmartTabsWithUrl`

## 0.1.23 от 17.03.2021

-  [fix]: `small_components`: Поправлена вёрстка `Banner` (ширина)
-  [feat]: `suggestions`: Для групп возвращает `title` вместо `slug`

## 0.1.22 от 03.03.2021

-  [feat]: `small_components`: Немного поправлена вёрстка `Banner`

## 0.1.21 от 03.03.2021

-  [fix]: `small_components`: Задан цвет из переменной для `UserName`
-  [feat]: `small_components`: Добавлены компоненты `ButtonLink`, `Banner`, `TimedBanner`
-  [feat]: `react_hoks`: Добавлен хук `useLocalStorage`
-  [feat]: `http`: Для BaseApi добавлена возможность перехватывать все стадии запроса

## 0.1.20 от 21.01.2021

-  [fix]: `forms2`: Убран `disabled` для полей во время валидации (фокус теряется)

## 0.1.19 от 18.01.2021

-  [feat]: `forms2`: Поддержка нескольких строк в `FormErrors`
-  [feat]: `http`: Передача аргументов в виде объекта в `BaseApi.request`
-  [feat]: `http`: Возможность не указывать apiPrefix для `BaseApi`

## 0.1.18 от 21.12.2020

-  [feat]: `forms2`: Для подписей задан `min-width`
-  [feat]: `http`: Поддержка передачи именованных параметров в `BaseApi.request()`
-  [feat]: `form_inputs`: Новый компонент `TimeZonePicker`
-  [fix]: `small_components`: Исправлен data-e2e селектор для `Pagination`

## 0.1.17 от 08.12.2020

-  [feat]: `forms2`: Новый тип поля: SuggestSelectField
-  [feat]: `suggestions`: Новый стиль для поля ввода запроса (view=default)
-  [feat]: `small_components`: Добавлен компонент `ExternalLink`
-  [feat]: `form_inputs`: Для `RoundedInput` добавлено свойство `useRenderDetails`
-  [feat]: `form_inputs`: Поддержка read-only для `RoundedInput`
-  [feat]: `form_inputs`: Поддержка `data-test` атрибута для `InputField`

## 0.1.16 от 16.10.2020

-  [feat]: `small_components`: ExternalLink

## 0.1.15 от 02.10.2020

-  [feat]: `metrika`: Возможность задать свой конфиг

## 0.1.14-beta.4 от 22.09.2020

-  [feat]: `modals`: Приведения дизайна ModalLayout в соответствие с макетами
-  [feat]: `modals`: Поддержка выравнивания по центру
-  [feat]: `modals`: BREAKING CHANGE! Поддержка передачи сложных опции при открытии модального окна
-  [feat]: `http`: Не добавляется заголовок X-CSRF-TOKEN для пустого токена

## 0.1.14-beta.3 от 18.09.2020

-  [feat]: `forms2`: Для `DurationField` добавлена возможность использовать миллисекунды в качестве базовой единицы

## 0.1.14-beta.1 от 11.09.2020

-  [feat]: `forms2`: Добавлен компонент FormErrors для вывода валидационных ошибок сразу по нескольким полям

## 0.1.13 от 10.09.2020

-  [feat]: `utils`: Добавлена утилита record для валидации словарей (динамических объектов)
-  [feat]: `polyfills`: Добавлен String.prototype.replaceAll. Полифилы теперь берутся из `core-js`
-  [chore]: `forms2`: Для InputControlProps добавлено наследование от ControlProps

## 0.1.12 от 01.09.2020

-  [fix]: `form_inputs`: Исправлен поиск в DropdownCheckboxList (не устанавливался фокус)

## 0.1.11 от 24.08.2020

-  [feat]: `small_components`: Ссылки на группы в UserName теперь формируются внутренним алгоритмом, а не запрашиваются

## 0.1.10 от 19.08.2020

-  [feat]: `_polyfills`: Добавлен полифил `Promise.allSettled`
-  [feat]: `form_inputs`: BytesInput, show rounded value

## 0.1.9 от 17.08.2020

-  [feat]: `forms2`: Добавлено свойство `FieldLayout.hideErrors`

## 0.1.8-alpha.1 от 13.08.2020

-  [fix]: `small_components`: Для Hint исправлена иконка
-  [fix]: `form_inputs`: Для RoundedInput добавлена поддержка пустых значений. Запрет на отрицательные значения
-  [fix]: `form_inputs`: Для OptionalNumber улучшено поведение при вводе пустых значений
-  [feat]: `small_components`: Возможность отключения глобальных хоткеев для Pagination

## 0.1.7-api-parse-error от 12.08.2020

-  [feat]: `http`: Возможность гибко спарсить ошибку из ответа

## 0.1.7 от 12.08.2020

-  [feat]: `forms2`: Поддержка disableIndeterminate для CheckboxField

## 0.1.6 от 30.07.2020

-  [fix]: `form_inputs`: DateTimePicker, исправлен ручной ввод времени

## 0.1.5 от 20.07.2020

-  [feat]: `form_inputs`: Для DateTimePicker добавлена возможность выводить время с секундами

## 0.1.3 от 15.06.2020

Удалён модуль `query_input` (будет извлечен в отдельный пакет). Вмержены все доработки из стабильных веток.

## 0.1.0-alpha.88 от 15.06.2020

-  [refactor]: `helpers`: Оптимизированы `isEmpty` и `isEqual`

## 0.1.2 от 02.06.2020

-  [feat]: `all`: Интеграция в проект data-ui/commons, фикс стилей
-  [refactor]: `small_components`: Pagination переписан

## 0.1.1 от 02.06.2020

Комбинированный релиз 0.1.0 + 0.1.0-alpha.86 + 0.1.0-alpha.87

## 0.1.0-alpha.87 от 02.06.2020

-  [feat]: `lego_wrappers`: Добавились обёртки для базовых лего-компонентов (кнопки, поля форм и т.п.)
-  [refactor]: `all`: Переход на использование `lego_wrappers` везде, где это возможно
-  [refactor]: `all`: Использование fixedMemo вместо React.memo
-  [feat]: `small_components`: Обновлён внешний вид Pagination
-  [feat]: `forms2`: Улучшена типизация ExtendedFieldConfig и useExtendedFieldConfig
-  [feat]: `form_inputs`: Добавлен компонент RoundedInput и обёртки для него DurationInput, BytesInput
-  [feat]: `forms2`: Добавлены поля DurationField, BytesField
-  [style]: `small_components`: Обновлена иконка для Hint

## 0.1.0-alpha.86 от 27.05.2020

-  [fix]: `form_inputs`: DropdownCheckboxList теперь закрывается после выбора, если multiple === false
-  [feat]: `small_components`: Новая тема подcветки в Json, добавлена поддержка свойства hidePre для скрытия рамки
-  [feat]: `styles`: Класс legoError добавлен в styleHelpers (для подсветки полей Lego с ошибками)

## 0.1.0 от 22.05.2020

-  [feat]: `query_input`: Добавлен модуль, компонент QueryInput для ввода сложных запросов в соотвествии с кастомной
   грамматикой (редактор кода по сути)

## 0.1.0-alpha.85 от 21.05.2020

-  [feat]: `models`: Добавлен интерфейс BaseInputProps для единообразных пропсов кастомных контролов ввода
-  [feat]: `form_inputs`: Добавлен компонент SetValuesInput
-  [feat]: `forms2`: Поддержка ReactNode для help полей
-  [feat]: `forms2`: Добавлено новое полеSetField
-  [refactor]: `forms2`: EnumField теперь построен на основе EnumSwitcher
-  [chore]: `form_inputs`: Правки вёрстки OptionalNumberInput

## 0.1.0-alpha.84 от 13.05.2020

-  [feat]: `small_components`: Добавлены компоненты Json, DevJson (с подсветкой)
-  [feat]: `small_components`: Hint теперь вместо html принимает ReactNode
-  [feat]: `utils`: Добавлен fixedMemo утилита - замена React.memo (только с правильным отображением в React Developer
   Tools)
-  [feat]: `form_inputs`: Добавлены компоненты OptionalNumberInput, EnumSwitcher
-  [feat]: `form_inputs`: Для EnumField в качестве title теперь можно передавать ReactNode (JSX)
-  [feat]: `forms2`: В качестве hint полей формы теперь можно передавать ReactNode (JSX)
-  [feat]: `forms2`: Добавлен компонент DevForm для отладки форм во время разработки

-  [feat]: Внедрён `prettier`, в том числе в pre-commit хук
-  [chore]: Весь код переформатирован в соответствии с настройками prettier

## 0.1.0-alpha.83 от 14.04.2020

-  [fix]: `form_inputs`: Множественные улучшения в `DropdownCheckboxList`

## 0.1.0-alpha.82-fix1 от 03.04.2020

-  [fix]: `forms2`: Поддержка вложенных ошибок валидации

## 0.1.0-alpha.82 от 03.04.2020

-  [fix]: `modals`: Вызов cancel при клике вне модалке (раньше просто пряталась)

## 0.1.0-alpha.81 от 10.03.2020

-  [fix]: `form_inputs`: Поддержка установки `null` извне для `DataTimePicker`
-  [fix]: `suggestions`: Запрет автозаполнения для `SuggestSelect` (в Blink-браузерах налезает на попап с вариантами)
-  [fix]: `forms2`: Поддержка хуков формы для `EnumField`
-  [feat]: `forms2`: Добавлена поддержка вертикального лайаута для форм (подписи сверху, а не сбоку)

## 0.1.0-alpha.80 от 04.03.2020

-  [feat]: `modals`: Теперь тип результата выводится из компонента, нет необходимости в явном указании типа для
   modalService.open(...)
-  [fix]: `http`: Теперь для GET-запросов preflight запросы не требуются. В том числе для Suggest API.
-  [new]: `forms2`: Новый модуль для работы с формами. Теперь на основе formik. Старый модуль deprecated.
-  [feat]: `suggestions`: Поддержка `SuggestSelect.clearOnClose` пропа
-  [chore]: Для некоторых компонентов добавлены селекторы для E2E тестов
-  [chore]: Обновлены все зависимости, обновлены правила линтера

## 0.1.0-alpha.79.2 от 14.02.2020

-  [fix]: `small_components`: `UserName` теперь использует `url`, если передан

## 0.1.0-alpha.79 от 14.02.2020

-  [fix]: `suggestions`: Запросы в Suggestion API теперь через прокси на `/external_api/suggest`

## 0.1.0-alpha.78.forms.2 от 22.01.2020

Технический релиз. В процессе добавляются разметка для E2E. Возможно фиксятся мелкие баги.

## 0.1.0-alpha.78.forms от 22.01.2020

-  [feat] `forms2`: Влиты изменения из ветки develop (актуализировано)

## 0.1.0-alpha.78 от 10.01.2020

-  [fix]: `small_components`: Отработка отсутствия аватарки на сервере
-  [feat]: `helpers`: getSetDifference теперь возвращать и список не изменившихся элементов (`unchanged`)
-  [feat]: `small_components`: CheckboxSelection теперь может работать с числовыми ID

## 0.1.0-alpha.77 от 09.01.2020

-  [fix]: `form_inputs`: Страница больше не скролится при открытии DropdownCheckboxList (вернул фокус)
-  [feat]: `small_components`: Логический компонент для выделения элементов в списках и таблицах

## 0.1.0-alpha.76 от 30.12.2019

-  [fix]: `form_inputs`: Страница больше не скролится при открытии DropdownCheckboxList

## 0.1.0-alpha.75.7 от 10.12.2019

-  [fix]: `forms`: Не вызывается onChange, если изменений в поле не было

## 0.1.0-alpha.75.6 от 10.12.2019

-  [feat]: `small_components`: Поддержка произвольных "системных" пользователей

## 0.1.0-alpha.75.5 от 09.12.2019

-  [fix]: `http`: Исправлена обработка не-JSON ответов при ожидании JSON
-  [chore]: Обновлены все зависимости

## 0.1.0-alpha.75.forms от 06.12.2019

-  [feat] `forms2`: Новый модуль форм на основе Formik

## 0.1.0-alpha.75.3 от 06.12.2019

-  [chore]: Обновлены все зависимости

## 0.1.0-alpha.75.2 от 25.11.2019

-  [feat] `http`: Поддержка кэширования в localStorage

## 0.1.0-alpha.74 от 22.11.2019

-  [fix] `utils`: Невалидационные ошибки при валидации теперь пробрасываются наверх
-  [feat] `forms`: Подсветка полей с ошибками
-  [feat] `forms`: Ширина подписей и контролов теперь фиксирована
-  [feat] `forms`: Короткие пояснения (hint) теперь выводится сразу под подписью, а не в popup
-  [feat] `react_hooks`: Добавлено несколько кастомных хуков (из Wall-E)
-  [feat] `utils`: Добавлены несколько утилит для валидации
-  [feat] `helpers`: Добавлены хелперы addSetItem и replaceItem
-  [feat] `small_components`: Компонент CopyableText

## 0.1.0-alpha.73 от 06.11.2019

-  [feat] `helpers`: Хелпер для определения различий между двумя Set getSetDifference

## 0.1.0-alpha.72 от 01.11.2019

-  [fix] `http`: Регресс 0.1.0-alpha.70 при пустом ответе сервера

## 0.1.0-alpha.71 от 07.10.2019

-  [fix] `http`: Регресс 0.1.0-alpha.70: Странные ошибки в Safari и FF

## 0.1.0-alpha.70 от 04.10.2019

-  [feat] `http`: Не пытается распарсить JSON в ответе, если он пуст.

## 0.1.0-alpha.69 от 02.10.2019

-  [feat] `actions`: Перед каждой ошибкой теперь пишется к чему она относится

## 0.1.0-alpha.68 от 20.09.2019

-  [tests] `all`: Добавил несколько селекторов для E2E

## 0.1.0-alpha.67 от 20.09.2019

-  [fix] `modals`: Теперь все модалки зафиксированы по вертикали, чтобы избежать прыжков при изменении высоты
-  [refactor] `small_components`: Добавил несколько селекторов для E2E

## 0.1.0-alpha.65 от 16.09.2019

-  [chore] `form_inputs`: `DateTimePicker` не обновляет дату при обновлении значения извне

## 0.1.0-alpha.63 от 16.09.2019

-  [chore] `forms`: `NumberField` теперь не использует `formatNumber` в состоянии read-only
-  [chore]: Обновлены все зависимости

## 0.1.0-alpha.62 от 10.09.2019

-  [fix] `form_inputs`: `DateRangePicker` по умолчанию использует начало и конец дня, а не текущее время

## 0.1.0-alpha.61 от 06.09.2019

-  [fix] `form_inputs`: Опциональный показ времени для `DateTimePicker`

## 0.1.0-alpha.60 от 29.08.2019

-  [fix] `suggestions`: Исправлено кэширование результатов

## 0.1.0-alpha.59 от 27.08.2019

-  [fix] `suggestions`: Глубоко переработан `SuggestSelect`, исправлено несколько багов
-  [fix] `forms`: `onChange` для полей теперь мемоизируется
-  [feat] `suggestions`: Добавлена утилита `getWeightedSuggestion`

## 0.1.0-alpha.58 от 26.08.2019

-  [feat] `small_components`: Добавлен компонент с формой обратной связи `FeedbackButton`

## 0.1.0-alpha.56 от 19.08.2019

-  [feat] `form_inputs`: Быстрый поиск в DropdownCheckboxList
-  [chore]: Обновлены все зависимости

## 0.1.0-alpha.55 от 16.08.2019

-  [fix] `small_components`: Фикс обрезания блока по числу строк `ClampLines` в Safari

## 0.1.0-alpha.54 от 12.08.2019

-  [feat] `suggestions`: Убрана магия с добавлением `@` к группам. Кажется, это особенность Walle, поэтому её не место в
   библиотеке.
-  [feat] `small_components`: Убрана поддержка распознавания `@` в `UserName` и `UserList`. Теперь эти компоненты
   работают с массивами объектов, где явно указан тип.

## 0.1.0-alpha.53 от 09.08.2019

-  [feat] `suggestions`: Новый слой `Issues`
-  [feat] `forms`: Новый тип поля `NumberSet`

## 0.1.0-alpha.52 от 07.08.2019

-  [feat] `suggestions`: `SelectSelect.allowEmptyQuery`

## 0.1.0-alpha.51 от 07.08.2019

-  [fix] `forms`: Значение NaN теперь очищается в `clearParams`
-  [fix] `suggestions`: Не учитывалось возможное отсутствие сущности для `stategy.getQueryFromEntity`
-  [feat] `suggestions`: Новый слой `Queues` (очереди в Трекере)

## 0.1.0-alpha.50 от 18.07.2019

-  [fix] `helpers`: Округление дат в `toQuery`
-  [fix] `form_inputs`: Некорректная мемоизация в `CheckboxItem`

## 0.1.0-alpha.49 от 17.07.2019

-  [feat] `small_components`: `LazyDropdown.onChangeOpened` теперь вызывается правильно

## 0.1.0-alpha.48 от 10.07.2019

-  [feat] `small_components`: Новый компонент `UserList`, поддерживающий группы

## 0.1.0-alpha.47 от 10.07.2019

-  [feat] `suggestions`: Добавлен слой `PeopleOrGroup`
-  [feat] `small_components`: Добавлено свойство `LazyDropdown.onOpenedChange`

## 0.1.0-alpha.46 от 08.07.2019

-  [feat] `suggestions`: Добавлено свойство `SuggestSelect.allowCreate`

## 0.1.0-alpha.45 от 08.07.2019

-  [feat] `small_components`: Хвостик `LazyDropdown` теперь сдвигается влево, в случае, если `switcher` нулевой ширины
-  [feat] `toasts`: Сообщение об успехе теперь зелёного цвета

## 0.1.0-alpha.43 от 04.07.2019

-  [feat] `small_components`: `Pagination` обзавёлся кнопками первая/последняя страницы

## 0.1.0-alpha.42 от 03.07.2019

-  [fix] `suggestions`: Исправлен баг с бесконечным запросом подсказок

## 0.1.0-alpha.41 от 29.06.2019

-  [fix] `forms`: Иконка `Hint` отрывается от подписи к полям (переносится одна на следующую строку)

## 0.1.0-alpha.40 от 28.06.2019

-  [feat] `small_components`: Для `LazyDropdown` добавлена возможность открывать его из-вне.

## 0.1.0-alpha.39 от 27.06.2019

-  [feat] `forms`: Расширена валидация форм

## 0.1.0-alpha.38 от 21.06.2019

-  [feat] `suggestions`: Возможность стирать значение
-  [fix] `suggestions`: Циклический запрос подсказок (бесконечный)
-  [feat] `modals`: Возможность блокировать закрытие окна по ESC или клику по backdrop
-  [chore] `deps`: Обновил все зависимости

## 0.1.0-alpha.37 от 18.06.2019

-  [new] `actions`: Возможность дизейблить отдельные кнопки в `ActionButtons`

## 0.1.0-alpha.36 от 17.06.2019

-  [new] `form_inputs`: Возможность показать ссылку в `CheckboxList`
-  [new] `_styles`: Стили для внутренних ссылок (в виде двух звеньев цепи) в `styleHelpers`

## 0.1.0-alpha.35 от 14.06.2019

-  [new] `actions`: Хранение дополнительного конфига для Action
-  [new] `actions`: Передача в поле значения всей формы `formValue`

## 0.1.0-alpha.34 от 10.06.2019

-  [fix] `actions`: Передача `meta` в компонент формы
-  [fix] `helpers`: `fillSetFields` теперь для несуществующих поле проставляет значение `new Set()`

## 0.1.0-alpha.32 от 10.06.2019

-  [fix] `small_components`: Поддержка `view=default`
   в `Pagination` [#INFRACLOUDUI-29](https://st.yandex-team.ru/INFRACLOUDUI-29)

## 0.1.0-alpha.31 от 06.06.2019

-  [fix] `_styles`: Внешние ссылки теперь подсвечиваются правильно (теперь точно)
-  [chore] `deps`: Обновил все зависимости

## 0.1.0-alpha.30 от 05.06.2019

-  [fix] `_styles`: Внешние ссылки теперь подсвечиваются правильно
-  [fix] `small_components`: Подсказка про горячие клавиши для `Pagination`

## 0.1.0-alpha.29 от 28.05.2019

-  [fix] `hotkeys`: Горячие клавиши игнорируются, если в фокусе `textarea`
   или `input` [#WALLEUI-413](https://st.yandex-team.ru/WALLEUI-413)

## 0.1.0-alpha.28 от 28.05.2019

-  [fix] `http`: Теперь метод `BaseApi.handleError` принимает полный Response и сообщение об ошибке (с сервера)

## 0.1.0-alpha.27 от 27.05.2019

-  [fix] `http`: Теперь метод `BaseApi.handleError` принимает полный Response
-  [fix] `toasts`: Экспорт моделей

## 0.1.0-alpha.26 от 27.05.2019

-  [fix] `suggestions`: Не запрашиваются подсказки при пустом запросе
-  [fix] `suggestions`: Отслеживаются изменения в свойстве `initialQuery`
-  [fix] `small_components`: `Avatar` в подсказках теперь не обрезается
-  [new] `small_components`: `Rows` теперь отрабатывает пустые строки как обрывы `<br>`

## 0.1.0-alpha.24 от 21.05.2019

-  [new] `suggestions`: Утилита `getSuggestion` для локальной оптимизированной выборки
-  [new] `suggestions`: Свойство `SuggestSelect.onQueryUpdate`

## 0.1.0-alpha.22 от 20.05.2019

-  [new] `form_inputs`: Свойство `withTime` для `DateRangePicker`
-  [new] `form_inputs`: Свойство `name` для `DropdownCheckboxList`

## 0.1.0-alpha.21 от 13.05.2019

-  [new] `form_inputs`: `DateTimePicker` поддерживает `size`
-  [fix] `react_hooks`: `useUrlUpdater` не учитывал `?` в начале `location.search`

## 0.1.0-alpha.19 от 13.05.2019

-  [fix] `forms`: `label` теперь необязательный
-  [chore] `deps`: Обновил все зависимости

## 0.1.0-alpha.18 от 7.05.2019

-  [new] `forms`: Добавил кнопку очистки полей `StringField`, `TextField`, `StringSetField`
-  [fix] `forms`: Использовал проверку `isEmpty` для значений в `clearParams`
-  [fix] `forms`: Добавил возможность передавать контекст в `clearParams`
-  [fix] `small_components`: Для `AccentFirstLetter` нужно использовать `::first-letter` в CSS

## 0.1.0-alpha.16 от 26.04.2019

-  [fix] `_styles`: Ошибка в цветовой палитре для тёмно-красного цвета

## 0.1.0-alpha.15 от 26.04.2019

-  [new] `forms`: Новый тип поля `HiddenField`
-  [new] `forms`: Утилита `clearParams` для очистки модели форма для отправки на сервер

## 0.1.0-alpha.14 от 26.04.2019

-  [new] Новый компонент `Rows` для вывода многострочного текста на основе массива или строки с `\n`;
-  [fix] Фикс вывода длинной ошибки в окне массовых операций

## 0.1.0-alpha.12 от 24.04.2019

Поддержка `readonly` режима в формах. Новые поля для форм: `Date`, `DateTime`, `StringSet`.

## 0.1.0-alpha.11 от 24.04.2019

Улучшил выполнение операций в `actions`, теперь они ограничены пятью одновременными. Переработал индикатор выполнения,
он показывает статус каждой операции.

## 0.1.0-alpha.10 от 23.04.2019

Обновил зависимости, добавил больше документации.

## 0.1.0-alpha.5 от 19.04.2019

Первая рабочая версия, пока без документации.
