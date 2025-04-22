[Тестирование ваншота](howto-testing.md) <br/>
[Доставка ваншота в продакшен](howto-release.md) <br/>
[Запуск ваншота](howto-launch.md) <br/>

# Как написать код ваншота

## Проверьте, подходит ли ваншот для вашей задачи

[Проверьте](concept.md#goals), подходит ли ваншотилка для вашей задачи или лучше подойдет другой инструмент.


## Создайте пакет для ваншота

Создайте новый пакет в модуле `direct/oneshot/` внутри пакета
[ru.yandex.direct.oneshot.oneshots](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/).
Придумайте короткое и ёмкое имя, например `oneshots/removesitelinks`.


## Создайте класс ваншота

Если ваншот будет работать с данными из базы [ppc](https://direct-dev.yandex-team.ru/db/ppc/index.html), то вам подойдет шардированный ваншот. В противном случае — обычный.

Шардированные ваншоты запускаются в отдельных потоках на каждый шард.

Имплементируйте один из интерфейсов:

- для шардированного ваншота — [ShardedOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/ShardedOneshot.java)
- для обычного — [SimpleOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/SimpleOneshot.java)

Полное имя класса ваншота будет его уникальным идентификатором в веб-интерфейсе, поэтому постарайтесь придумать ему такое имя, чтобы не путать с другими ваншотами. <br/>
Хороший пример: `~.generatesmartcreatives.GenerateSmartCreativesOneshot`. <br/>
Плохой пример: `~.creative.UpdateCreatives`.

Или расширьте один из базовых классов:
- для обычного ваншота без входных данных и состояний - [SimpleOneshotWithoutInput](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/base/SimpleOneshotWithoutInput.java)
- для обычного ваншота без входныз данных, но с состояниями - [SimpleIterativeOneshotWithoutInput](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/base/SimpleIterativeOneshotWithoutInput.java)
- для шардированного ваншота без входных данных - [ShardedOneshotWithoutInput](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/base/ShardedOneshotWithoutInput.java)
- для шардированного ваншота без входныз данных, но с состояниями - [ShardedIterativeOneshotWithoutInput](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/base/ShardedIterativeOneshotWithoutInput.java)

- для ваншота, работающего с YT - [YtOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/yt/YtOneshot.java)

## Сделайте ваншот видимым для Spring

Поставьте аннотацию `@Component` (`org.springframework.stereotype.Component`). Так ваншот станет спринговым синглтоном.

## Выберите тип ваншота { #choose-oneshot-type }
Ваншоты делятся на обычные и безопасные. В большинстве случаев достаточно обычного ваншота, который будет проходить стадию апрува для запуска.

Если выбрали безопасный ваншот, то необходимо добавить аннотацию [@SafeOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/SafeOneshot.java) к классу. Такие ваншоты не требуют апрува и могут запускаться любым разработчиком.

Концепция безопсаного ваншота описана [тут](./concept#safe-oneshot)

Также при попадании такого ваншота в релиз будет создан специальный тикет на ревью, который попадает акцептору для проверки.


## Определите список апруверов для обычных ваншотов {#approvers}

{% note info %}

Для безопасных ваншотов данный пункт можно пропустить.

{% endnote %}

Для каждого запуска ваншота вам потребуется подтверждение от другого разработчика.

Определите список коллег, которые смогут подтверждать запуски. Каждый из них должен удовлетворять следующим условиям:

- он понимает что делает ваншот и связанные с этим риски;
- он понимает, когда (и с какими входными данными) можно запускать ваншот, а когда нельзя;
- он должен быть разработчиком (не менеджером).

На роль апрувера хорошо подходят старшие коллеги, техлид или руководитель.

Поставьте аннотацию [@Approvers](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/Approvers.java), указав список апруверов в виде логинов на [staff.yandex-team.ru](https://staff.yandex-team.ru).


## Зафиксируйте, будет ли ваншот многоразовым или одноразовым

Если повторный запуск ваншота может нанести вред, то ваншот должен быть одноразовым. Таким он будет по умолчанию.

Если же вы планируете запускать ваншот многократно и/или уверены в безопасности повторного запуска, то поставьте аннотацию [@Multilaunch](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/Multilaunch.java).


## Перезапуски итераций { #retries }

Если итерации (происходящее внутри метода `execute`) можно перезапускать при вылете исключений (например сеть мигнула),
то поставьте аннотацию [@Retries](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/Retries.java).
Задайте в ней разрешенное число повторов.
Также можно указать атрибут `timeoutSeconds` — паузу между перезапусками (по умолчанию 30 секунд).


## Поведение при падении { #pause-instead-of-fail }

Если ваншот можно перезапускать (повторный запуск на тех же данных не приводит к конфликтам или дублям), то можно поставить анотацию
[@PausedStatusOnFail](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/worker/def/PausedStatusOnFail.java).
С ней при падении потока выполнения (и исчерпании ретраев, если заданы) запуск ваншота перейдет в статус **Paused**,
из которого его можно будет запустить вручную:
- без повторного апрува
- с того же момента, на котором остановилось выполнение (см. `prevState` у метода `execute`).

Это удобно в ситуациях, когда ожидаемые проблемы можно исправить вручную (например поправить битые данные миграцией).


## Создайте класс входных данных

Ваншотилка поддерживает передачу входных данных в ваншот при запуске в веб-интерфейсе ([прод](https://direct.yandex.ru/internal_tools/#oneshots) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshots)). Это позволяет делать гибкие многоразовые ваншоты.

Если вам не потребуется при запуске ваншота передавать ему входные данные, то в качестве generic-параметра `V` укажите `Void`. Посмотрите [пример](#example_no-input_no-state) ваншота без входных данных.

Как научить ваншот принимать входные данные:

1. Создайте POJO для входных данных. Убедитесь, что у него есть дефолтный конструктор, а поля не объявлены `final`, чтобы `Gson` смог создать экземпляр.
2. Укажите этот класс в качестве generic-параметра V, тогда объект входных данных будет передаваться в методы `validate` и `execute` в качестве параметра `inputData`.

Посмотрите [пример](#example_input_no-state) ваншота с входными данными.


## Реализуйте валидацию входных данных

При запуске ваншота входные данные будут передаваться через поле в веб-интерфейсе в виде json-строки. Сначала они попадут в метод `validate`, и только в случае успешной валидации будет вызван метод `execute`.

Реализуйте код валидации в методе `validate` с помощью библиотеки валидации.

{% note warning %}

Метод `validate` не должен изменять данные в базе.

{% endnote %}

Если ваншот не принимает входные данные (принимает `Void`) или валидация не требуется, верните пустой результат валидации:
```java
@Override
public ValidationResult<Void, Defect> validate(Void inputData) {
    return ValidationResult.success(inputData);
}
```


## Реализуйте полезную логику ваншота

Реализуйте полезную логику ваншота в методе `execute`.

Метод `execute` вызывается только в случае успешного прохождения валидации в методе `validate`.

{% note tip %}

Используйте по возможности продакшеновый код ядра.

{% endnote %}

{% note tip %}

Используйте Spring для подключения компонентов ядра и всех его зависимостей.

{% endnote %}

{% note warning %}

Для хранения состояния используйте только локальные переменные метода `execute`. В полях класса состояние хранить нельзя, так как ваншот создается как спринговый синглтон.

{% endnote %}


## Если ваншот будет выполняться долго, сделайте его итеративным

Если прогнозируемое время выполнения ваншота составляет до 10 минут, то вам не требуется реализовывать итеративный ваншот. Укажите `Void` в качестве generic-параметра `S`, а из метода `execute` просто возвращайте `null`. Посмотрите [пример](#example_no-input_no-state) неитеративного ваншота.

Если прогнозируемое время выполнения ваншота составляет более 10 минут, тогда сделайте его работу итеративной с использованием нативных инструментов ваншотилки (а не с помощью цикла в методе `execute`).<br/>Для чего это нужно:

- вы сможете отслеживать состояние выполнения ваншота на странице потоков выполнения ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launch_data) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launch_data));
- ваншот можно будет поставить на паузу и затем возобновить (например, для выкладки нового релиза ваншотилки).

Как это работает. Вы реализуете в методе `execute` только одну итерацию. При первом запуске метод принимает `null` в качестве параметра `prevState`, таким образом можно понять, что это стартовая точка. После выполнения первой итерации метод должен заполнить определенный вами кастомный объект состояния и отдать его ваншотилке в качестве возвращаемого значения. При следующем вызове метода `execute` ему будет передан этот объект, и он сможет продолжить работу. Когда вся полезная работа выполнена, метод должен вернуть `null`, таким образом ваншотилка понимает, что это была последняя итерация.

Пошаговая инструкция:

1. Создайте POJO для хранения состояния. Убедитесь, что у него есть дефолтный конструктор, а поля не объявлены `final`, чтобы `Gson` смог создать экземпляр.
2. укажите этот класс в качестве generic-параметра `S`;
3. реализуйте код метода `execute` таким образом, чтобы он выполнял одну итерацию полезной работы на основе этого состояния и возвращал обновленное состояние;
  - метод должен уметь принимать `null` для первой итерации;
  - метод должен возвращать `null`, когда вся работа выполнена;

Готово! теперь ваш ваншот умеет выполняться итеративно, а вы можете отслеживать текущее состояние на странице потоков выполнения ([прод](https://direct.yandex.ru/internal_tools/#oneshot_launch_data) | [ТС](https://test-direct.yandex.ru/internal_tools/#oneshot_launch_data)), приостанавливать и возобновлять его выполнение.

Посмотрите [пример](#example_no-input_state) итеративного ваншота.

{% note tip %}

Используйте в качестве состояния простые объекты. Так будет проще визуально наблюдать за состоянием в веб-интерфейсе. К тому же, размер колонки для хранения состояния ограничен.

Это может быть объект, содержащий идентификатор последней обработанной записи (потребуется сортировка). На практике чаще всего нет необходимости делать что-то более сложное.

{% endnote %}

## Примеры

### Неитеративный ваншот без входных данных {#example_no-input_no-state}

```java
@Component
@Multilaunch
@Approvers({"mexicano"})
public class OneshotWithoutInput implements SimpleOneshotWithoutInput {

    @Override
    public ValidationResult<Void, Defect> validate(Void inputData) {
        return ValidationResult.success(inputData);
    }

    @Override
    public Void execute(Void inputData, Void state) {
        // делаем полезную работу
        return null;
    }
}
```

### Неитеративный ваншот с входными данными {#example_input_no-state}

```java
@Component
@Multilaunch
@Approvers({"mexicano"})
public class OneshotWithInput implements SimpleOneshot<InputData, Void> {

    @Override
    public ValidationResult<InputData, Defect> validate(InputData inputData) {
        ItemValidationBuilder<InputData, Defect> ivb = ItemValidationBuilder.of(inputData);
        ivb.item(inputData.getIds(), "ids")
                .check(notNull());
        return ivb.getResult();
    }

    @Override
    public Void execute(InputData inputData, Void state) {
        doUsefulWork(inputData.getIds());
        return null;
    }
}

public class InputData {

    private List<Long> ids;

    public List<Long> getIds() {
        return ids;
    }

    public void setIds(List<Long> ids) {
        this.ids = ids;
    }
}
```

### Итеративный ваншот без входных данных {#example_no-input_state}

```java
public class IterativeOneshot implements SimpleIterativeOneshotWithoutInput<State> {
    private static final int MAX_ITERATION_SIZE = 100;


    @Override
    public State execute(State state) {
        List<Long> sortedIds = getSortedIds();

        // в первой итерации state == null, в этом случае начинаем обрабатывать id с 0-й позиции в списке sortedIds
        int startPosition = state == null ? 0 : state.getPosition();
        int endPosition = state.getPosition() + MAX_ITERATION_SIZE;

        // получаем список id, который будем обрабатывать в текущей итерации
        List<Long> idsForProcessing = sortedIds.subList(startPosition, endPosition);

        // выполняем полезную работу
        doWork(idsForProcessing);

        // если обработали весь список, то возвращаем null, и на этом выполнение ваншота остановится,
        // в противном случае возвращаем позицию для следующего вызова execute
        if (endPosition >= sortedIds.size()) {
            return null;
        } else {
            return new State().withPosition(endPosition);
        }
    }
}

public class State {

    // в качестве состояния будем использовать позицию в упорядоченном списке идентификаторов, обрабатываемых ваншотом
    private Integer position;

    public Integer getPosition() {
        return position;
    }

    public void setPosition(Integer position) {
        this.position = position;
    }
}
```

### Примеры в Аркадии

- [Все боевые ваншоты лежат здесь](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots)
- [Простой пример нешардированного ваншота](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/simple/TestSimpleOneshot.java)
- [Простой пример шардированного ваншота](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/sharded/TestShardedOneshot.java)

- [Пример ваншота использующего YT](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/invalidpermalinks/InvalidPermalinksOneshot.java)

## Дополнительная информация

Есть пример ваншота по изменению стратегий в кампании.
В ревью есть [хороший комментарий](https://a.yandex-team.ru/review/1263673/details#comment--3395835) от Саши Дуплищева, как писать подобные ваншоты (арканум не всегда скроллит к нужному комменту, ищите самый длинный ;) )
Позже это вероятно войдет в how-to.
