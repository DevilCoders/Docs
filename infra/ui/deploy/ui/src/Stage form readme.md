# Форма стейджа. Базовая структура и принципы работы

## Мотивация

Описанная ниже архитектура была создана для решения трех больших проблем:

1. Невозможность отрисовки огромных стейджей целиком. Слишком много нод, и DOM просто не позволял нормально их отрисовать.
2. Необходимо обеспечить нормальную навигацию по огромному стейджу с возможностей синхронизации с URL'ом.
3. Хотелось переиспользовать решения при переделке Няни.

## Структура

### HugeForm

**Куда смотреть**: ui/src/components/huge-form

Движок, который отвечает исключительно за рендеринг дерева, операции с узлами, синхронизация изменений с редаксом.

Просто низкоуровневая отрисовка. Он не привязан ни к каким моделям данных и ничего не знает об уровнях вложенности.

Задача компонента HugeForm - принять в себя данные (необязательно иерархические) в пропсе _value_ и разложить по уровням вложенности в соответствии с конфигом уровней из пропса _levelConfigs_.

**Внутреннее устройство HugeForm**

В основе лежит библиотека для работы с формами [Formik](https://formik.org/docs/overview).

Структурно компонент состоит из компонента SideTree, который рисует уровни в левой части, и роутов, сгенерированных на основе конфига уровней и данных, которые будут рисоваться в виде форм в основной части.

Чтобы получить список форм для левой части, используется хук _useFormsFromValue_, который лежит в /ui/src/components/huge-form/hooks.

Роуты для правой части получаются на основе _levelConfigs_ из пропсов.

Компонент для роута получается через HOC _formHOC_. Именно этот компонент отвечает за генерацию форм для Formik'а.
Какой компонент будет отображаться внутри Formik'а, пробрасывается из поля _component_ в конфиге уровня.

Также HugeForm от классических форм на Formik'е отличается использованием внутри компонента FormLocalState. Он предназначен для синхронизации изменений состояния формы с редаксом.

Formik by design хранит текущее состояние формы в своем внутреннем стейте, и доступа к нему мы не имеем, поэтому если нам нужно дернуть какой-то метод при изменении пропсов формы, то мы должны создать компонент, который принципиально устроен следующим образом:

-  в качестве пропсов он принимает состояние формы и методы, которые мы должны вызывать при изменении этого состояния;
-  при каких-то манипуляциях с формой мы сравниваем новое и старое состояния формы;
-  если в результате сравнения мы решили, что нам нужно прикопать изменения во внешнем стейте, мы дергаем соответствующий метод. В данном случае это методы _onChange_ и _onRevert_

Этот способ является общим для всех случаев, когда нам нужно вытаскивать наружу сосотояние формы до сабмита.

Вытаскивать стейт из Formik'а наружу нам требуется потому, что непосредственно в Formik'е мы рендерим только часть всего стейджа, относящуюся только к одной сущности (Stage, DU, Box, Workload) с указанным id, и изменения в этой сущности нам необходимо сохранять в стейте в редаксе.

Как такового сабмита в Formik'е при этом не происходит.

Если нам для работы формы нужны какие-то дополнительные данные, не содержащиеся в _value_, мы их прокидываем через пропс _payload_, который потом пробрасывается в контекст HugeForm.

### Конвертация спеки

**Куда смотреть**: ui/src/models/ui/stage

Спека стейджа плоская. Workload'ы и Box'ы идут в данных вперемешку и никакой вложенности друг в друга не поддерживают, поэтому чтобы на UI работать со спекой как с нормальным деревом, мы вынуждены производить конвертацию "сырой" спеки с удобное для UI дерево.

Т.о. в течение жизненного цикла компонента мы имеем следующие преобразования:

1. Спека стейджа преобразуется в UI-модель, имеющую древовидную структуру.
2. UI-модель уже внутри HugeForm разбирается на формы.
3. Формы редактируются.
4. При сохранении HugeForm из своих форм собирает измененную UI-модель.
5. Измененная UI-модель конвертируется в новую спеку.

В папке хранится логика конвертации данных для каждого из уровней. На примере, боксов

_Папка_: ui/src/models/ui/stage/Box

_Box.ts_ - UI-модель бокса. Там же хранится объект с дефолтными значениями, которые будут подставляться при создании нового бокса.

_BoxConverter.ts_ - конвертер, который конвертирует данные бокса из спеки в UI-модель бокса. Метод _toJSON_ возвращает нам сконвертированную модель.

_BoxPatcher.ts_ - патчер, который используется для патчинга боксов. Патчит спеку в соответствии с новыми значениями бокса. Он необходим для того, чтобы не перезатереть в спеке параметры, которые не поддерживаются в UI-модели бокса. Именно из-за этих параметров мы вынуждены патчить исходную спеку вместо того, чтобы просто сконвертировать новую из UI-модели.

Метод патчера _toValue_ превращает UI-модель бокса в модель спеки, описанную в протобафе. Методы _patchSomething_ патчат конкретные типы данных.

### Конфигурация уровня

**Куда смотреть**: ui/src/components/stage-levels

Конфигурация уровня задает, как мы отрисовываем каждый уровень модели. Уровни связывают воедино UI-модель стейджа и HugeForm.

Важные пропсы в конфиге уровня:

-  clearOnClone - функция, которая удаляет в UI-модели бокса связи с другими сущностями при его клонировании;
-  component - непосредственно набор полей, которые будут рендериться внутри Formik'овской формы;
-  getEmptyValue - функция, возвращающая дефолты, которые подставляются при создании новой сущности;
-  formParamsToValue - функция, которая превращает параметры формы Formik'овские в UI-модель;
-  valueToFormParams - наоборот, UI-модель в параметры формы;
-  getChildren - логика получения детей из родителя;
-  id - идентификатор уровня;
-  level - уровень визуального отображения в дереве (отступ);
-  routePath - часть урла, которая генерится для уровня;
-  validationSchema - схема валидации полей для формы данной сущности. Формик для этого использует [yup](https://github.com/jquense/yup).

**Форма для component**

В ней используются те же библиотечные компоненты, что и при отрисовке других форм на Formik'е. Если нам нужно нарисовать что-то более сложное.
Например, вложенный набор полей, то значения для них оборачиваются в библиотечный компонент FieldLayout2 (см. в документацию в нашей либе).

## Типовые сценарии

### Добавить какое-то поле на форму

1. Добавляем поле в UI-модель сущности для уровня (Stage, DU, Box, WL)
2. Добавляем извлечение этого поля из спеки в конвертере
3. Добавляем поле в параметры формы, которая будет его отрисовывать
4. Добавляем правила валидации этого поля формы в схему
5. Добавляем прокидывание этого поля в пропсы формы в методе valueToFormParams в конфиге левела
6. Добавляем извлечение этого поля из формы в методе formParamsToValue
7. Добавляем логику патчинга спеки в патчер
