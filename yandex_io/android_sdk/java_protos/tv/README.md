## Description

Models from this directory are used for IPC between iosdk-app and client apps.

Abstractions on this layer mostly repeat abstractions and structures from IOSDK,
but we decided to do it this way to keep application-level IPC independent from
IOSDK's structures.

Also, additional software layer gives us more control over IPC compatibility.

IMPORTANT: This IPC should be backward and forward compatible, to ensure that if two apps
belong to the same generation, they interact properly (or at least gracefully fail).

## Content

audiosdk.proto - models used by YandexIoAudioSdk
alicesdk.proto - models used by YandexIoAliceSdk
binder.proto - models used for binder interactions
