# Draft полокационная выкладка

## Задача/Проблема
В Яндексе существует правило, что все сервисы (за редким исключением) должны переживать -1 DC.
Текущая гранулярность выкладки и отсутствие ручного контроля значительно увеличивает вероятность аварии.

## Решаемые проблемы
Увеличить гранулярность выкладки до 1 ДЦ.
Дать возможность ручного контроля за выкладкой по ДЦ.
Изменения затрагивают только **per cluster replica set controller (rsc)**

## Проблемы, которые мы не решаем
В рамках текущего документа мы не затрагиваем функционал **multi replica set controller (mrsc)**
При необходимости это будет выполнено отдельным документом.

## Варианты решения
Компонентом, в котором происходит генерация и синхронизация конфигураций для ДЦ контроллеров, является stage_ctl.
Соотвественно, основная часть дискуссии это как и в каком виде донести до него данные о настройках выкладки по ДЦ и аппрувах.

### Варианты решения задачи где хранятся параметры:
#### 1. Использовать лейблы
**Минусы:**

1. Ограниченность в типе и схеме данных без дополнительной реализации
1. Нет возможности получить историю изменения
1. Нецелевое использование

**Плюсы:**

1. Быстрая реализация
1. Отсутствие завязки на релизный цикл YP

#### 2. Хранить параметры в спеке.
**Минусы:**

1. Медленная интеграция.
1. Более сложная миграция в случае изменение схемы (миграция схемы YP с добавлением колонки)

**Плюсы:**

1. Полноценные типы и схемы данных
1. Историчность привязана к спеке

### Варианты решения задачи с апрувами:
#### 1. Хранить данные аппрувов в текущей колонке статуса.
**Минусы:**

1. Конкурентная модификация статуса с stage_ctl
1. Разрешение пользователю запись в статус (без предварительной правильной настройки ACE (access control entry), это может быть проблемой)

**Плюсы:**

1. Быстрая реализация

#### 2. Хранить данные в текущей колонке статуса но модифицировать их через контролы.
**Минусы:**

1. Конкурентная модификация статуса с stage_ctl.
1. Более сложная реализация (написание кода /control )

**Плюсы:**

1. Можно настроить отдельные доступы на контролы
1. Нет необходимости открывать статус на запись

#### 3. Хранить данные в отдельной колонке и модифицировать их через контролы.
**Минусы:**

1. Наиболее сложная реализация и соотвественно поддержка. (миграция YP для использования новой колонки, написание кода /control)

**Плюсы:**

1. Можно настроить отдельные доступы на контролы
1. Нет необходимости открывать статус на запись
1. Отсутствие конкуренции на модификацию одной колонки со stage_ctl

## Выбранное решение
Для хранения настроек выкладки наиболее полноценное и масштабируемое решение это решение с хранением данных в спеке **#2**.

Для аппрувов - решение **#3**, так как оно перекрывает все минусы предыдущих и выглядит как более перспективное не только для аппрувов.

## Этапы реализации
Первым этапом мы делаем и интегрим простое решение с лейблами, это позволит нам быстро проитерироваться и написать необходимую базу для stage_ctl. Тем самым более частично решать задачу.
Плюс за время полноценной реализации пользователи смогут погонять функционал и принести проблемы.

Вторым этапом является уже полноценная реализация в соответствии с выбранным решением.

Лог дисскуссий по дизайну в тикете [https://st.yandex-team.ru/DEPLOY-3381](https://st.yandex-team.ru/DEPLOY-3381) и  [pull-request](https://a.yandex-team.ru/review/1466544/details)

## Внедрение
**В UI**
Можно использовать текущий блок настройки локаций в настройках DeployUnit

По галочке "Катить полокационно" разблокировать изменение порядка блоков настройки конкретной локации. В сами блоки добавить галочку "Требуется аппрув".

Для аппрува хорошо подходит главная страница со сводной информацией DeployUnit, кнопки Approve\Disapprove можно разместить в самих блоках статуса выкладки кластера.

**Консольный клиент**
Для того чтобы настроить полокационную выкладку, удобнее всего будет использовать dctl, для этого в первом варианте достаточно добавить нужный лейбл с порядком кластеров, во втором варианте пропатчить нужными параметрами спеку.

С аппрувами несколько сложнее так как для них используются контролы.

На текущий момент использование контролов возможно только yp клиентом. При необходимости можно научить dctl пушить в контролы, для этого логичнее всего расширить dctl put, добавив в него control, с параметрами стейджа и пути к фалу в формате yml с параметрами контрола. [https://st.yandex-team.ru/DEPLOY-3647](https://st.yandex-team.ru/DEPLOY-3647)

Готовность кластера правильнее всего делать, проверив статус rsc в конкретной локации через dctl.

[Пользовательская документация с тикетами на дополнительные работы](perlocation.md)

