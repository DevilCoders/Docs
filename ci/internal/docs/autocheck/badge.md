# Плашка

Плашка отображает статистику сравнения работы тестов на левой и правой ревизии, может состоять из одного или нескольких
контуров. При падении одного из контуров, вся плашка считается упавшей.

Статистика в быстром и полном контуре разбита на две группы: основная и дополнительная. Контур считается упавшим если
есть новые падения в основной статистике, Strong mode или Broken by deps.

## Основная статистика

Основная статистика состоит из следующих категорий:

* Configure – конфигурации.
* Build – сборки.
* Style – проверки стиля.
* Small tests – маленькие тесты.
* Medium – средние тесты.

Для каждой категории плашки отображаются группы чисел слева направо: пройденные, упавшие, пропущенные. Если в группе
есть второе число с плюсом, значит этот тест изменил свой статус. Например, если в Build в упавших будет +1, значит есть
сборка, которая в левом запуске успешна или отсутствует, а в правом упала.

## Дополнительная статистика

Дополнительная статистика состоит из следующих категорий:

* Timeout – тесты, не успевшие выполниться за отведенное время слева или справа.
* Muted – тесты с падениями, по которым отключены уведомления.
* Internal – тесты с внутренними падениями автосборки.
* External – тесты с падениями, имеющие тег external.
* Flaky – тесты, которые имеют разный статус на разных запусках одной ревизии (левой или правой).
* Broken by deps – тесты упавшие из-за падений в модулях, от которых он зависит.
* Strong mode – тесты имеющие падения и попадающие под режим обязательной проверки для автора проверки.
* Added – добавленные или перемещенные тесты, у которых отсутствует статус слева.
* Deleted – удаленные или перемещенные тесты, у которых отсутствует статус справа.

### Timeout

Timeout тесты без включенного Strong mode не влияют на статус плашки, так как в общем случае невозможно определить, был
ли этот таймаут из-за ошибки в коде или тест просто слишком долго выполняется. Несмотря на то, что они не влияют на
статус плашки, их полезно иногда просматривать. Например, если изменение затрагивает небольшое количество тестов, но
появляется большое количество новых таймаутов, то это может свидетельствовать о том, что таймауты вызваны именно правкой
кода.

### Muted

Уведомления по тестам отключаются автомьютилкой, если тест работает нестабильно. Это делается для того, чтобы эти
нестабильные тесты не мешали разработчикам видеть действительно новые падения, а не флапы. Если вы хотите видеть падения
по своим тестам, с отключенными уведомлениями, вам следует включить Strong Mode. Затем хорошим тоном будет исправить эти
тесты так, чтобы они выдавали стабильный результат, тогда автомьютилка вновь включит по ним уведомления.

## Internal

Внутренние падения автосборочной машинерии. Если возникает новое такое падение, следует обратить в
очередь [DEVTOOLSSUPPORT](https://st.yandex-team.ru/DEVTOOLSSUPPORT)

## External

External тесты – это тесты, которые имеют тег external и имеют возможность ходить по сети. Так как сеть может работать
нестабильно, эти тесты могут менять свой статус на одной ревизии. Они не влияют на статус плашки, так как нет
возможности определить, чем вызвано падение.

## Flaky

Flaky тесты – это тесты, которые имеют разный статус на одной и той же ревизии в разных запусках. Таким тестам
автомьютилка сразу отключает уведомления и они переходят в категорию Muted в последующих проверках.

