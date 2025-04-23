### IntelliJ IDEA
Сгенерировать файл проекта zk-queue.ipr можно так:

    ya make --checkout
    ya ide idea --project-root=.

# ZkQueue
Highly available queue implementation over Apache Zookeeper.

## Motivation

In some cases there is a need for highly available distributed queue with 
not so high throughput requirements. 
It is possible to use Apache Zookeeper for fine grained queue implementation.

This is especially handy when there already exists a supported ZK cluster 
and separate queue solution is an overkill (our scenario).

## When NOT to use
This queue will feel okay when the maximum size is limited by multiple thousands of messages.
If the rate of messages is going to be a lot higher, another solution should be considered.

https://cwiki.apache.org/confluence/display/CURATOR/TN4

## What will be implemented in first version

* ✔ Multiple consumers with correct failover.
* ✔ Local transactions: you can consume N elements and produce K elements within one transaction.
* ✔ FIFO semantic is sacrificed to decrease consumer contention.
* ✔ Flexible consuming policy control.
* ✔ `MessageListenerContainer`-like interface for switching from Spring.
* ✔ Each queue will have its own internal DLQ.
* ✔ Ability to chose at-least-once semantic.

## What to expect next
 
* ✗ Priorities can be assigned to queue items with best effort guarantees.
* ✗ Backoff policies on redelivery.
* ✗ Strict FIFO semantic.

## Usage

When the simple queue interface is all you need, it is possible to use `ZkQueue` directly.

```java
queue = new ZkQueue(...);
queue.init(); // create directories

try (UnitOfWork tx = queue.newTransaction()) { // if tx is not committed, it will be rolled back
    final Optional<String> item = tx.tryTake(inputDestination); // the element is locked here
    tx.put(outputDestination, "Hello, " + item); // actual writing happens on tx commit
    tx.commit(); // it will atomically remove consumed item and write new one
}

queue.close(); // close connection to zk

```

If you want to connect to some queue and invoke a listener for each input message, the right class is `QueueListenerContainer`.
It works similar to Spring `DefaultMessageListenerContainer`. Usually this will dramatically simplify error handling.

Usage:
```java
listener = (consumer, m) -> consumer.putOnCommit(outputDestination, "Hello, " + m)

final QueueListenerContainer container = new QueueListenerContainer(..., listener);
container.start(); // here the listener starts serving input messages
```

## Architecture overview

Items are created and stored as persistent sequental znodes. When the item is consumed within transaction, the lock is
created as ephemeral znode and it prevents other transactions from consuming the same item. On transaction commit locks 
are removed together with elements and new items are created. Commit happens atomically via Curator transaction.

When client dies or disconnects, ephemeral znodes disappear and other consumers can take previously locked items.

```
.
└──zms
   ├── queue1
   │   ├── items
   │   │   ├── item-0000000001 // actual queue payload
   │   │   └── item-0000000002
   │   ├── locks
   │   │   ├── lock-0000000001 // element locks
   │   │   └── lock-0000000001_363bc583-8384-40a5-af11-acb5e50f1ead // protection from partial failures
   │   ├── meta
   │   │   ├── meta-0000000001 // info for redelivery
   │   │   └── meta-0000000002
   │   └── dlq 
   │       └── item-0000000042 // this element was rejected by redelivery policy
   └── queue2
       └── ...
```

## Guarantees

* If `tx.commit()` returns without exception, the TX is committed.
* `tx.rollback()` always succeeds and guarantees to remove all locks and cancel all `put()` operations.
* `try-with-resources` on `UnitOfWork` instance will rollback non-committed transaction.
* Client session expiration will remove all locks in single transaction.
* Thread interruption can leave TX in inconsistent state. 
Subsequent `rollback()` call guarantees to succeed and correctly rollback the TX. 
However, if `rollback()` operation is interrupted, it is aborted immediately without any guarantees.
The motivation for this behavior is that `rollback()` operation should be interrupted only when application
stops and all ZK locks will expire anyway. 
* Consuming policy `ConsumeTimes(K)` guarantees to consume the element at most `K` times.
This implies `ConsumeOnce()` guarantees to consume the element at most once.

## Implementation details

### ZkUnitOfWork
Single transaction. All queue operations should be done within transaction. The transaction is bound to the single Zookeeper session.
If the session is expired, no further operations are possible with this transaction and new one should be created.
Multiple transactions will share the same session for performance reasons.
 
Consuming the element with `tryTake()` method locks the element and does not remove it.
`put()` operation records the element in memory and does not make any network calls.
`commit()` operation atomically removes all taken elements with locks and creates new elements.
The transaction should not be huge because there is a limitation of 1MB size from Zookeeper.

`rollback()` operation attempts to unlock all elements or to observe session expiration.
When the connection is lost, `rollback()` can take session timeout time to complete, but it guarantees to
succeed at some point and to leave no locks behind.

All operations are synchronized and can be called from different threads.

### ZkQueue
Queue instance. Manages connection to Zookeeper and creates `ZkUnitOfWork`. Ensures that connection to ZK is made in
a correct way (with few mandatory hacks). The instance is not bound to single destination.

Usually whole application will have single `ZkQueue` instance. However, multiple instances of this class does not affect
each other. Queue closing will close the connection to Zookeeper and this will invalidate all produced transactions.

All operations are synchronized and can be called from different threads.

### QueueListenerContainer
Class similar to Spring's `DefaultMessageListenerContainer`. It uses ZkQueue instance, listens to particular destination and
distributes messages across worker threads.

Any exception in listener will cause transaction to be rolled back. Network issues and session expirations also 
rollback the transaction. Listener should correctly survive network flaps and be resilent.

Closing the `QueueListenerContainer` will shut down thread pools. It should be done only on application close because
interruted `rollback` operation does not guarantee anything and may leave hanging locks. Please note, container closing
does not close underlying `ZkQueue`.
