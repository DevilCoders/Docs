---
title: Workflow library
rank: 50
---

## Библиотека Workflow для описания процессов

Библиотека workflow предоставляет примитивы для описания работы транзакционных процессов. Библиотека предоставляет следующие примитивы
- [`Workflow`](#Worklfow) - actor-подобная конструкция, транзакционно читающая сообщения из очереди, связанной с этим workflow и вызывающая в транзакции обработчик, соответствующий этому сообщению
- [`TaskProcessor`](#TaskProcessor) - вспомогательный класс для описания фоновых процессов
- [`SingleRunOperation`](#SingleRunOperation) - конструкция, поверх Workflow для одноразовых операций в стиле fire-and-forget с дополнительной возможностью запуска в заданный момент времени

### Master, Hot-Standby

Задеплоенные сервисы, построенные с использованием библиотеки `workflow` работают в режиме, когда один узел кластера выбирается мастером (`master`), а остальные находятся в режиме ожидания (`hot-standby`).
Удобно думать об этом так: `master` выполняет `rw` запросы, `hot-standby` может выполнять `ro` запросы, а так же помещать сообщения в очередь `Workfow`*.

Инстанс сервиса становится мастером, если ему удается захватить lock в базе postgresql (см. [`DBMasterLockManager`](https://a.yandex-team.ru/arc_vcs/travel/library/java/master-lock-manager/src/main/java/ru/yandex/travel/workflow/ha/DBMasterLockManager.java)). После захвата лока, спустя заданный конфигурацией промежуток времени инстанс мастера оживляет запущенные на нем `WorkflowProcessService`, `TaskProcessor`-ы.
При потере лока, инстанс приостанавливает работу запущенных на нем `WorkflowProcessService`-а и `TaskProcessor`-ов. Если их работа не может быть приостановлена за заданное конфигурацией время, все открытые этими сервисами транзакции автоматом переключаются в режим `rollback-only`.

### Workflow

`Workflow` - сущность, содержащая идентификатор и тип сущности, к которой прикреплена очередь с сообщениями. Сообщения описываются `proto` структурами.
`WorkflowProcessService` постоянно отслеживает появление новых сообщений для `Workflow`. При появлении нового сообщения, сервис в транзакции по типу сущности, ассоциированной с данным `Workflow` находит handler (инстанс `WorkflowEventHandler`), и вызывает его с соответствующим сообщением, дополнительно передавая контекст (`MessagingContext`) вызова, созданный с помощью `MessagingContextFactory`, за счет чего в контекст обработки передается закрепленная к `Workflow` сущность.
Для удобства написания конечного автомата с использованием `Workflow` существуют различные реализации `WorkflowEventHandler`, наиболее распространенная в использовании `ProxyStateMapWorkflowEventHandler`, который позволяет описать различный `WorkflowEventHandler`-ы в зависимости от сущности типа `WorkflowEntity`, находящейся в контексте выполненя сообщения.

### TaskProcessor

Сервис, который позволяет запускать фоновые процессы. Состоит из двух частей
- поток, постоянно вычитывающий в базе ключи задач, ожидающих обработки
- пул обработчиков, каждый из которых ожидает на вход ключ и реализует логику обработки ключа
(e.g. `TaskProcessor`, вычитывающий операции, ожидающие выполнения, и обработчик, который для соответствующей операции помещает в очередь ее закрепленного `Workflow` сообщение вида `TCommit`).

### SingleRunOperation

Простая операция, которую можно запустить в стиле `fire-and-forget`
Для реализации простой операции необходимо реализовать `SingleOperationRunner` и зарегистировать соответствующий тип операции в инстансе `SingleOperationRunnerProvider`.

[Пример использования в сервисе заказов](https://a.yandex-team.ru/arc_vcs/travel/orders/app/src/main/java/ru/yandex/travel/orders/configurations/OperationsConfiguration.java)


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


