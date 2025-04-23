%%(plantuml)
@startuml
cloud "AliceServer" {
  [AliceScenarios]
}

package "Quasar Services" {
  [State Service]
  [Alice] --> onAudioData
  [Alice] --> alice_toggleConversation
  [Alice] -->[AliceScenarios]
  [Media Player] --> mediaPlayPause
  [BluetoothService] ..> BluetoothInterface
  note top of [BluetoothService] : Uses Bluetooth Impl Provided by vendor
 
}

package "SDK Client" {
  [AudioSource] --> sdkPushAudioData
  [AudioSource] ..> onAudioData
  [Sdk Interface] --> sdkNotifyMuteState
  [Sdk Interface] --> toggleConversation
  [Sdk Interface] ..> alice_toggleConversation
  [Sdk Interface] ..> onSdkState
  [Sdk Interface] --> provideSdkState
}

package "Linux" {
  [ALSA] --> alsa_pcm_capture
  [ALSA] --> alsa_pcm_play
  [DevInput] --> key_events
  [led_interface] --> play_leds
}

package "Vendor" {
  alsa_pcm_capture ..> [AudioInputController]
  [AudioInputController] ..> sdkPushAudioData
  [AudioInputController] ..> onMicsState
  [AudioInputController] --> mute_unmute

  key_events ..> [ButtonsHandler]
  [ButtonsHandler] ..> mute_unmute
  [ButtonsHandler] ..> sdkNotifyMuteState
  [ButtonsHandler] ..> volumeUp_volumeDown
  [ButtonsHandler] ..> toggleConversation
  [ButtonsHandler] ..> mediaPlayPause

  [VolumeManager] --> volumeUp_volumeDown
  [VolumeManager] ..> playAnimation

  [LedManager] --> playAnimation
  [LedManager] ..> play_leds

  [DeviceStateHandler] --> onMicsState
  [DeviceStateHandler] --> onSdkState
  [DeviceStateHandler] ..> playAnimation

  [BluetoothImpl] --> BluetoothInterface : provide bt impl

}

[Media Player] ..> alsa_pcm_play
[State Service]  ..> provideSdkState

@enduml
%%

Notation

%%(plantuml)
@startuml
[component1] --> interface1 : component1 provide interface1
[component2] ..> interface1 : component2 uses interface1
@enduml
%%

