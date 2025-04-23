# Approximate scheme of YandexIO Services

%%(plantuml)
@startuml
package "YandexIO Services" {
  [Alice]
  note top of [Alice] : Keep connection with Alice clout, Process WakeupWord, Control DialogState
  [MediaPlayer]
  note top of [MediaPlayer] : Play .mp3/.wav local files, play .mp3 from url, play HLS stream
  [Alarms_Notifications]
  note bottom of [Alarms_Notifications] : Manage user Timers/Alarms. Manage Alice notifications
  [Calls]
  note bottom of [Calls] : Manage Yandex Calls
  [Configuration]
  note bottom of [Configuration] : Manage Device Configuration state (handle sound configuration)
  [Bluetooth]
  note bottom of [Bluetooth] : Manage Bluetooth using Vendor Provided Bluetooth implementation
  [Wifi]
  note top of [Wifi] : Manage wifi via WpaSupplicant api
  [Updater]
  note bottom of [Updater] : Manage Updates. Download OTA from Yandex server. Apply OTA via vendor custom script  

@enduml
%%

