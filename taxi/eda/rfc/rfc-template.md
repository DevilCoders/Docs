@startuml
[*] --> State1
State1 --> [*]
State1 : this is a string
State1 : this is another string
State1 -> State2
State2 --> [*]
@enduml





@startuml firstDiagram

Alice -> Bob: Hello
Bob -> Alice: Hi!

@enduml