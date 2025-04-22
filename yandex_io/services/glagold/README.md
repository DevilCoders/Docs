# Glagold
<!-- toc generated with https://github.com/ekalinin/github-markdown-toc -->
   * [Glagold](#glagold)
      * [Workflow](#workflow)
      * [Incoming json messages format](#incoming-json-messages-format)
         * [ping](#ping)
         * [serverAction](#serveraction)
         * [rewind](#rewind)
         * [play](#play)
         * [next](#next)
         * [prev](#prev)
         * [stop](#stop)
         * [setVolume](#setvolume)
         * [control](#control)
         * [externalCommandBypass](#externalcommandbypass)
         * [aliceStateBypass](#alicestatebypass)
         * [showAliceVisualState](#showalicevisualstate)
         * [leaderOverrideBypass](#leaderoverridebypass)
         * [playMusic](#playmusic)
         * [sendText](#sendtext)
      * [Outgoing json messages format](#outgoing-json-messages-format)
         * [controlState section](#controlstate-section)
         * [playerState section](#playerstate-section)

## Workflow
Exposes itself as a WebSocket endpoint on devices. Receives different json messages, converts some into protobuf objects and sends to corresponding services.
Also responsible for sending services states back to WebSocket clients.

Incoming messages should be signed with JWT token, which can be got from backend URL: `/glagol/token?device_id=DEVICE_ID&platform=PLATFORM`.

Glagold WebSocket server checks each message against set of verified tokens which are cached on device side. If token is not in set - tries to verify it on backend side `/glagol/check_token` and cache it after.
If received token is wrong/empty/expired - the ws connection will be closed with `Websocket::StatusCode::INVALID_TOKEN` code and Metrica `invalid_jwt_token` will be reported.
Each valid WebSocket message will be followed with `valid_jwt_token` event reported to Metrica.

## Incoming json messages format
```json
{
  "conversationToken": "<TOKEN>",
  "payload": {
    "command": "<COMMAND>",
    ...
  }
}
```
### ping
```json
{
  "command": "ping"
}
```
Just a simple ping. Checks connection and no other logic triggered.

### serverAction
```json
{
  "serverActionEventPayload": {
    "type": "server_action",
    "name": "update_form",
    "payload": {
      "form_update": {
        "name": "personal_assistant.scenarios.get_news",
        "slots": [
          {
            "name": "topic",
            "optional": true,
            "type": "news_topic",
            "value": "business"
          }
        ]
      },
      "resubmit": true
    }
  },
  "command": "serverAction"
}
```
Sends custom server action to `aliced`. Action payload should be passed in `serverActionEventPayload` field. Waits for response from `aliced` and forwarding it back to the client.

### rewind
```json
{
  "command": "rewind",
  "position": 30.0
}
```
Rewinds player playback to specified second by sending corresponding message to `mediad`

### play
```json
{
  "command": "play"
}
```
Sends `player_continue` command to `aliced`

### next
```json
{
  "command": "next"
}
```
Sends `player_next_track` command to `aliced`

### prev
```json
{
  "command": "prev"
}
```
Sends `player_previous_track` command to `aliced`.

### stop
```json
{
  "command": "stop"
}
```
Sends `player_pause` command to `aliced`

### setVolume
```json
{
  "command": "setVolume",
  "volume": 0.4
}
```
Sends `sound_set_level` message to `aliced`. Volume should be passed as double in `[0, 1]` range. It will be multiplied by 10 as `volumed` expects it in a range of `[1, 10]`

### control
```json
{
  "command": "control",
  "action": "go_right",
  "scrollAmount": "exact",
  "scrollExactValue": 3
}
```
Responsible for sending navigation (control) commands to `interfaced` 
Glagol converts it to `QuasarMessage.ControlRequest` message and sends to `aliced`, where the message will be forwarded to `interfaced`.

Available values:
- `action` = `go_up`, `go_down`, `go_left`, `go_right`, `click_action`
- `scrollAmount` = `few`, `many`, `exact`, `till_end`
- `scrollExactValue` = integer

`scrollAmount` and `scrollExactValue` are optional and can be provided in addition to navigation commands in order to specify navigation details.
If no `scrollAmount` or `scrollExactValue` provided, it means interface should be scrolled by one screen or element - depends on interface logic implementation

### externalCommandBypass
```json
{
  "command": "externalCommandBypass",
  "data": "base_64_encoded_string"
}
```
Bypass message to `aliced` passed as base64 encoded string in `data` field. Protobuf `mutable_external_command()->ParseFromString` will be called against decoded string.
Glagol bypass response back to the client in `extra.bypassResponse` base64 encoded string. Response is always has `success` status.

### aliceStateBypass
```json
{
  "command": "aliceStateBypass",
  "data": "base_64_encoded_string"
}
```
This command is only sent from Leader device (not a Glagol app). Protobuf `mutable_external_alice_state()` will be constructed from decoded string and sent to `aliced`

### showAliceVisualState
```json
{
  "command": "aliceStateBypass",
  "aliceStateName": "LISTENING",
  "recognizedPhrase": "bla bla bla"
}
```
Sends corresponding `mutable_external_alice_state()` to `aliced`

### leaderOverrideBypass
```json
{
  "command": "leaderOverrideBypass",
  "data": "base_64_encoded_string"
}
```
This command is only sent from Leader device (not a Glagol app). Protobuf `mutable_leader_override()->ParseFromString` will be called against decoded string and sent to `mediad`

### playMusic
```json
{
  "command": "playMusic",
  "type": "track",
  "id": "4251965",
  "offset": 0.0
}
```
Sends play music command to `aliced` as a server action which comes from VINS (simulates it)

### sendText
```json
{
  "command": "sendText",
  "text": "домой"
}
```
Sends custom text command to `aliced` as a response which comes from VINS (simulates it)

### controlState section
Format of `state.controlState`:
```json
{
  "controlState" : {
      "hasUp": false,
      "hasDown": true,
      "hasLeft": true,
      "hasRight": false,
      "hasClickAction": false
   }
}
```
Describes available control commands on current screen.
If there is no `controlState` element - there are controls available for the given screen now

### playerState section
Format of `state.playerState`:
```json
{
  "playerState": {
    "duration": 190.09305,
    "extra": null,
    "hasNext": true,
    "hasPause": false,
    "hasPlay": true,
    "hasPrev": true,
    "hasProgressBar": true,
    "progress": 6.488523,
    "subtitle": "Woodkid",
    "title": "Iron",
    "liveStreamText": "прямой эфир"
  }
}
```
Describes available commands for media player and media info

### setOverridedChannel section
Force set sound channel for device in multiroom mode
```json
{
  "payload": {
    "command": "setOverridedChannel",
    "channel": "<channel name>"
   }
}
```
Supported channel names: "left", "right", "all" and "undefined". Any invalid name will be interpreted as "undefined"
