## Об использовании транзакций
В workflow каждое сообщение обрабатывается handler-ом в рамках транзакции.
Исторически, для работы с транзакциями мы использовали либо напрямую TransactionTemplate, либо помечали методы сервиса как @Transactional.

У нас было определенное количество сервисов, которые были помечены @Transactional(propagation=MANDATORY) это была подсказка, что сервис должен выполняться внутри транзакции, и дополнительно служило проверкой, что сервис не вызовут вне транзакции.

У использования такого @Transactional есть неприятный момент. Если использовать метод сервиса внутри try/catch блока, то отловленное исключение не предотвратит отката транзакции. Пример
```
class ServiceB {
    @Transactional(propagation=MANDATORY)
	void inner() {
	   throw new RuntimeException("Hey ho");
	}
}

class ServiceA {
   ServiceB serviceB;

   @Transactional(propagation=REQUIRES_NEW)
   void outer() {

      Order order = orderRepository.get(id);

      try {
         serviceB.inner();
      } catch (Exception e) {
         // some recover logic, including writing some data
         order.setErrorValue("THAT ONE IS NOT SAVED");
      }

   }
}
```
Вопреки ожиданиям, отлов ошибки не поможет, внешняя транзакция, которая была начата при вызове метода outer() будет помечена как rollback-only. И все данные, записанные после этого в сущность молча откатятся.

Почему так происходит?
Spring долгое время служил и до сих пор служит легкой альтернативой JavaEE. В JavaEE неявные исключения, выкинутые за пределы `@Transactional` приводят к пометке транзакции, как rollback-only.
Так у нас появилась аннотация `@TransactionMandatory`, которая просто проверяет, запущена ли транзакция.

Так же, для корректной работы JpaRepository в выбранной модели на уровне объявления `@SpringBootApplication` надо использовать `@EnableJpaRepositories(enableDefaultTransactions = false)`. О причинах так делать описано ниже (TL;DR в противном случае проблемы возникающие внутри сгененрированного кода репозитория будут так же неявным образом приводить к откату транзакций)

Во многих местах нашего кода используется Spring Data JPA. Удобная библиотека, которая генерирует CRUD сервисы и позволяет часто не писать руками запросы. Но есть один момент, который стоит учитывать.

Все сервисы, которые генерируются из объявленных Repository так или иначе наследуются от SimpleJpaRepository, у которого на самом классе и методах висит `@Transactional`. А в самих методах есть precondition проверки входящих параметров, которые выкидывают исключения. Поэтому НА ДАННЫЙ МОМЕНТ стоит внимательно относиться к вызовам CRUD методов JpaRepository.

Например вот такой код не самым явным для разработчика образом пометит транзакцию, как rollback-only.
```
class ServiceA {
   OrderRepository orderRepository;
   UserRepository userRepository;

   @Transactional(propagation=REQUIRES_NEW)
   void outer() {

      try {
          // we got a non null user id
          User user = userRepository.get(userId);
          // user is not null
          UUID orderId = getUUID();
          Order order = orderRepository.get(id);
      } catch (Exception e) {
         // some recover logic, including writing some data
         user.setStatus("Loser")
      }

   }

   void UUID getUUID() {
      // something went wrong and we return null;
      return null;
   }
}
```
