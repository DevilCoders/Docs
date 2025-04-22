@startuml
package "Входящий поток" {
[Receiving]
}

package "Хранение" {
[Placement]
[Picking]
[Inventoriztion]
}

package "Исходящий поток" {
[Consolidation]
[Packing]
[Dropping]
[Shipping]
}

cloud {
[Radiator]
}


database "MS SQL" {
[SCPRD]
}

database "Postgres" {
[SCPRD]
}

[Picking] --> [Consolidation]
[Consolidation] --> [Packing]
[Packing] --> [Dropping]
[Dropping] --> [Shipping]
@enduml
