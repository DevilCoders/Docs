%%(plantuml)
@startuml
package "SDK Components" {
  [AudioSource]
  note top of [AudioSource] : Forward AudioData provided by vendor to YandexIO Services
  [SDK Interface]
  note top of [SDK Interface] : Provide  Api to register SDK Observer implementations. Provide Api to control Dialog, Media Player, ... etc.
  [SDK Observers]
  note bottom of [SDK Observers] : Observers that used to notify SDK State(dialog, configuration, players state, etc...),  and events/directives

@enduml
%%
