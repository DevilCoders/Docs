# Библиотека валидации

### Общее описание

Библиотека состоит из двух частей:
- результаты валидации: пакет result.
- выполнение валидации (построение результатов валидации): пакет builder.

#### Результаты валидации

Результат валидации ValidationResult - иерархический, каждый узел соответствует
какому-то объекту, а его дочерние узлы - полям объекта или элементам списка.
Каждый результат валидации содержит валидируемое значение и списки ошибок
и предупреждений, которые могут быть пустыми, а так же ассоциативный массив
"путь" -> "результат валидации" для хранения дочерних узлов.

Библиотека не содержит классов для представления самих ошибок и предупреждений,
реализация этих классов целиком ложится на клиентский код.

У класса ValidationResult есть методы flattenErrors и flattenWarnings для
получения списков ошибок и предупреждений соответственно со всего поддерева в
виде объектов DefectInfo, каждый из которых содержит путь к валидируемому полю
относительно того узла, на котором вызван метод, провалидированное значение и
ошибку/предупреждение.

Класс ValidationResult не рекомендуется использовать непосредственно в клиентском коде
для осуществления валидации, для этой цели существуют классы из пакета builder:
ItemValidationResult и ListValidationResult, для проверки объектов и списков соответственно.


#### Выполнение валидации

Основные классы и интерфейсы для выполнения валидации:
- ItemValidationBuilder: содержит методы для валидации объектов
- ListValidationBuilder: содержит методы для валидации списков
- Constraint: ограничение, принимает объект и возвращает "дефект", реализация ложится на клиентский код
- ListConstraint: ограничение, принимает список и возвращает "дефекты" для отдельных элементов
- Validator: валидатор, принимает объект и возвращает ValidationResult
- When: интерфейс, позволяющий выполнить указанную проверку только при определенных условиях

Подробное описание классов смотрите в Javadoc.

Для использования библиотеки валидации необходимо:
- реализовать произвольный класс, представляющий "дефект", который будет выступать в роли ошибки или предупреждения
- реализовать ограничения, реализующие интерфейс Constraint, работающие с этим типом дефекта
- создавать экземпляры ItemValidationBuilder или ListValidationBuilder и использовать их методы check* для проверок


**Пример использования**

```java
// класс дефекта
public class DefectType {
    private int code;
    private String message;
}

// класс валидируемых объектов
public class Address {
    private String city;
    private Integer postcode;

    // getters/setters
}

// сервис валидации
public class AddressValidationService {

    public ValidationResult<List<Address>, DefectType> validate(List<Address> addressList) {
        Set<String> allCities = Cities.getAvailableCities();
        Set<Integer> allPostcodes = Postcodes.getAvailablePostcodes();

        ListValidationBuilder<Address, DefectType> validationBuilder =
                ListValidationBuilder.of(addressList);

        // здесь и далее подразумевается статический импорт констрейнтов из некоторого внешнего класса
        validationBuilder
                .check(notNull())
                .check(minListSize(1))
                .check(maxListSize(MAX_ADDRESS_LIST_SIZE))
                .checkEachBy(notNull())
                .checkEachBy(this::validateAddress, When.isValid());

        return validationBuilder.getResult();
    }

    public ValidationResult<Address, DefectType> validateAddress(Address address) {
        Set<String> allCities = Cities.getAvailableCities();
        Set<Integer> allPostcodes = Postcodes.getAvailablePostcodes();

        ItemValidationBuilder<Address, DefectType> validationBuilder =
                ItemValidationBuilder.of(address);

        validationBuilder.check(cityAndPostcodeIsConsistent());

        validationBuilder.item(address.getCity(), "city")
                .check(notNull())
                .check(notEmpty())
                .check(inSet(allCities), When.isValid());

        validationBuilder.item(address.getPostcode(), "postcode")
                .check(notNull())
                .check(greaterThan(0))
                .check(inSet(allPostcodes), When.isValid());

        return validationBuilder.getResult();
    }
}
```