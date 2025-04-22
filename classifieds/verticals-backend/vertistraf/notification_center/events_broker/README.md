# Брокер событий центра уведомлений[WIP]

## Что это
Сервис для вычитывания событий сервиса, важных для отправки пушей и отправки их в mindbox.

Примерная схема работы сервиса:
```mermaid
graph TD
    A1(Producer1) -->|Event| A{Composite producer}
    A2(...) -->|Event| A
    A3(ProducerN) -->|Event| A
    A -->|Event| B(CompositeProcessor)
    B -->|Event1| B1(Event1Processor)
    B -->|...| B2(...)
    B -->|EventN| B3(EventNProcessor)
    B1 -->|http| D1(MindboxHandler1)
    B2 -->|http| D2(...)
    B3 -->|http| D3(MindboxHandlerN)
```

### Проект в стадии запуска, отправка событий в mindbox пока не реализована
