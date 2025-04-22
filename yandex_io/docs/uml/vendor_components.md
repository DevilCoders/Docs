%%(plantuml)
@startuml
package "Vendor Components" {
  [AudioInputController]
  note top of [AudioInputController] : Capture Mic Data, Apply VQE, push data to SDK AudioSource
  [ButtonsHandler]
  note top of [ButtonsHandler] : Get Buttons Events, Call Internal/SDK Methods (change volume, toggleConversation, etc)
  [VolumeManager]
  note top of [VolumeManager] : Provide api for VolumeUp/VolumeDown. Implement setVolume methods(will be called by SDK)
  [LedManager]
  note bottom of [LedManager] : Draw animations via led interface. Provide api to play selected animation
  [BluetoothImpl]
  note bottom of [BluetoothImpl] : Implementation for sdk Bluetooth interface. This implementation will be provided to sdk
  [StateHandler]
  note bottom of [StateHandler] : Some Vendor state handler, that choose active LED animation. part of state is provided by SDK(i.e. AliceState), and some of state provided by vendor (i.e. MuteState)
@enduml
%%
