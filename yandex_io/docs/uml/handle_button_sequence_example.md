%%(plantuml)
@startuml
actor User
participant "Buttons" as Buttons << HW >>
participant "DevInputEvents" as DevInput << Linux >>
participant "ButtonsHandler" as ButtonsHandler << Vendor >>
participant "StateHandler" as StateHandler << Vendor >>
participant "YandexIOSDK" as YandexIOSDK << SDK Api >>
participant "Alice" as Alice << YandexIO Services >>
participant "Alice Server" as Server << Yandex Alice Cloud >>

User -> Buttons : Click Button
Buttons -> DevInput : Event
DevInput -> ButtonsHandler : Key Event
ButtonsHandler -> YandexIOSDK : Call startConversation
YandexIOSDK -> Alice : Call startConversation
Alice -> Alice : Change state (idle -> listening)
Alice -> Server : Start request (start send audio stream)
Alice -> YandexIOSDK : Send AliceState Listening
YandexIOSDK -> StateHandler : Notify new AliceState: Listening
StateHandler -> StateHandler : Handle new state (change led animation, etc...)
@enduml
%%

