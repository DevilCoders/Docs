%%(plantuml)
@startuml
actor User
participant "Mics" as Mics << HW >>
participant "ALSA" as ALSA << Kernel >>
participant "AudioInputController" as AudioInputController << Vendor >>
participant "VQE" as VQE << Vendor >>
participant "AudioSource" as AudioSource << SDK Api >>
participant "Alice" as Alice << YandexIO Services >>
participant "WakeUpWord" as WakeUpWord << YandexIO Services (Alice Component) >>
participant "Alice Server" as Server << Yandex Alice Cloud >>

User -> Mics : Sound
Mics -> ALSA : PCM
ALSA -> AudioInputController : PCM
AudioInputController -> VQE : PCM
VQE -> AudioSource : PCM
AudioSource -> Alice : PCM
Alice -> WakeUpWord : PCM
User --> WakeUpWord : Say Alice (trigger ww)
Alice <-- WakeUpWord : WW Triggered event
Alice -> Server : (ogg)
@enduml
%%
