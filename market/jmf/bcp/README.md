# Business Chain Processor

Модуль содержит сервис позволяющий в декларативном порядке описать список необходимых операции с бизнес-объектом, которые необходимо выполнить при
его модификации.

Рассмотрим простой пример:

Пусть у нас есть *Сотрудник* с атрибутами:
1) *firstName* (Петр, не обязателен);
2) *lastName* (Сидоров);
3) *title* (Сидоров Петр);
4) *creationTime*.

К дополнительным требования относятся: проверить права на создание объекта.

Мы хотим создать объект *Сотрудник*. Тогда код, реализующий создание объекта будет выглядеть следующим образом:

```java
class EmployeeService {
    
    SecurityService securityService;
    Dao dao;
    
    Employee create(String lastName, String firstName) {
        if (!securityService.hasPermission()) {
            throw new SecurityException();
        }
        
        Employee employee = new Employee();

        employee.setLastName(lastName);
        employee.setFirstName(firstName);
        employee.setTitle(lastName + " " + firstName);
        employee.setCreationTime(Instant.now());
        
        if (null == lastName) {
            throw ValidationException();
        }
        
        dao.save(employee);
    }
    
    Employee create(String lastName) {
        // все возможные комбинации параметров создаваемого объекта 
    }
    
}
```

Каждую функцию создания объекта из кода выше можно представить как последовательность простых операции:
1) Проверка прав;
2) Создание объекта;
3) Заполнение требуемых полей;
4) Проверка объекта;
5) Сохранение объекта.

Этот набор операции базовый, и не зависит от создаваемого объекта будь то *Сотрудник*, *Отдел* или *Контрагент*.

**[BcpService](src/main/java/ru/yandex/market/jmf/bcp/BcpService.java)** обеспечивает выполнение необходимых простых операций при создании,
модификации и удалении объектов и имеет простой интерфейс:

```java
public class BcpService {
     Entity create(Fqn fqn, Map<String, Object> properties) {}

     Entity edit(Entity entity, Map<String, Object> properties) {}

     Entity delete(Entity entity) {}
}
``` 

Пример конфигурации используемой по умолчанию для создания объектов:

```xml
    <b:domain id="@default">
        <b:process id="create">
            <b:requiredOperation>@create</b:requiredOperation>
            <b:requiredOperation>@save</b:requiredOperation>
            <b:requiredOperation>@validateRequiredAttributes</b:requiredOperation>
            <b:requiredOperation>@validateMetaclass</b:requiredOperation>
            <b:requiredOperation>@defaultValues</b:requiredOperation>

            <b:group id="init">
                <b:operations>
                    <b:operation id="@create"/>
                    <b:operation id="@defaultValues"/>
                    <b:operation id="@validateMetaclass"/>
                </b:operations>
            </b:group>
            <b:group id="processAttributes">
                <b:after>init</b:after>
                <b:operations>
                    <b:defaultOperation id="@default" bean="@setAttributeValue"/>
                    <b:operation id="metaclass" bean="@empty"/>
                </b:operations>
            </b:group>
            <b:group id="save">
                <b:after>processAttributes</b:after>
                <b:operations>
                    <b:operation id="@save"/>
                </b:operations>
            </b:group>
            <b:group id="validation">
                <b:after>save</b:after>
                <b:operations>
                    <b:operation id="@validateRequiredAttributes"/>
                </b:operations>
            </b:group>
            <b:group id="finalize">
                <b:after>validation</b:after>
                <b:operations>
                </b:operations>
            </b:group>
        </b:process>
    </b:domain>
```

Этой конфигурацией описывается процесс создания произвольного объекта (описанного метаинформацией). Здесь:

1) Указано, что в процессе создания всегда должны быть выполненные операции *@create*, *@save*, *@validateRequiredAttributes*,
 *@validateMetaclass*, *@defaultValues*.
2) Все операции разбиты на группы: *init*, *processAttributes*, *save*, *validation*, *finalize*. При этом задан прядок следования групп операции 
(см. *after*).
3) Операции *@create*, *@defaultValues*, *@validateMetaclass* относятся к группе *init*; операции *metaclass* и "@default" относится к группе
*processAttributes* и т.д.
4) *defaultOperation* - описывает все операции, которые не описаны явно.
5) У части операции указан атрибут *bean*, который ссылается на код бина, реализующий выполнение операции. У операции, у которых *bean* не указан,
 имя бина совпадает с id-операции.  

Рассмотрим пример кода:
```java
class Example {
    Entity doLogic() {
        bcpService.create("employee", ImmutableMap.of("lastName", "Сидоров"));
    }
}
```

Этим кодом мы хотим создать объект метакласса "employee" с запоненным атрибутом lastName. BCP понимает, что для создания объекта необходимо выполнить
операции *@create*, *@defaultValues*, *@validateMetaclass*, *lastName* (в конфигурации явно не описана. будет использована операция по умолчанию),
 *@save* и *@validateRequiredAttributes*. Порядок операции определяется заданным порядком в конфигурации.
 
При этом для конкретного метакласса можно доопределять набор операции и их порядок, например, для заполнения поля *title*, которое является
конкатенацией *lastName* и *firstName* мы можем определить операцию *title* следующим образом: 

```xml
    <b:domain id="employee">
        <b:process id="create">
            <b:group id="processAttributes">
                <b:operations>
                    <b:operation id="lastName" bean="@setAttributeValue">
                        <b:before required="true">title</b:before>
                    </b:operation>
                    <b:operation id="firstName" bean="@setAttributeValue">
                        <b:before required="true">title</b:before>
                    </b:operation>
                    <b:operation id="title" bean="@employeeTitle" />
                </b:operations>
            </b:group>
        </b:process>
    </b:domain>
```

Здесь бин *@employeeTitle* реализует логику конкатенации. Так же указано, что если выполняется операция *lastName* или *firstName*, то обязательно 
надо выполнить операцию *title*, что будет гарантировать непротиворечивость значения атрибута title у сотрудника.

Тот же пример можно переписать используя другой способ указания обязательности включения операции в процесс

```xml
    <b:domain id="employee">
        <b:process id="create">
            <b:group id="processAttributes">
                <b:operations>
                    <b:operation id="title" bean="@employeeTitle">
                        <b:after ifPresent="true">firstName</b:after>
                        <b:after ifPresent="true">lastName</b:after>
                    </b:operation>
                </b:operations>
            </b:group>
        </b:process>
    </b:domain>
```

Т.е. читать описание зависимостей операций нужно читать так:
- operationX `before & required` operationY - operationX будет выполнен раньше operationY. Если в процессе появится
operationX, то в этот же момент в процесс добавится operationY. Если в процессе появится operationY, то operationX 
не обязательно появится в процессе. Кто-то его должен явно добавить
- operationX `before & ifPresent` operationY - operationX будет выполнен раньше operationY. Если в процессе появится
operationY, то в этот же момент в процесс добавится operationX. Если в процессе появится operationX, то operationY
не обязательно появится в процессе. Кто-то его должен явно добавить
- operationX `after & required` operationY - operationX будет выполнен позже operationY. Если в процессе появится
operationX, то в этот же момент в процесс добавится operationY. Если в процессе появится operationY, то operationX 
не обязательно появится в процессе. Кто-то его должен явно добавить
- operationX `after & ifPresent` operationY - operationX будет выполнен позже operationY. Если в процессе появится
operationY, то в этот же момент в процесс добавится operationX. Если в процессе появится operationX, то operationY
не обязательно появится в процессе. Кто-то его должен явно добавить

## Отладка
Для отладки рекомендуется включать логирование. Имя логера имеет следующий формат:
```
bcp.{metaclass}.{edit|create|delete}
```

Например,
  - ``` bcp ``` включает логирование действий с объектами любых метаклассов;
  - ``` bcp.employee ``` включает логирование действий с объектами у которых метакласс employe (и для всех типов этого метакласса);
  - ``` bcp.employee.edit ``` включает логирование изменении объектов метакласса employee.
  
Замечание: на данный момент нельзя включить логирование только для конкретного типа, например, ``` employee@external ```.
