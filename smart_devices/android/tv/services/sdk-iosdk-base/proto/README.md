## Description

Models from this directory are used for IPC between some of services-iosdk-app and client apps.

Abstractions on this layer is used only inside services-iosdk-app services and client apps.
These proto models shouldn't refer to eny external models.

IMPORTANT: This IPC should be backward and forward compatible, to ensure that if two apps
belong to the same generation, they interact properly (or at least gracefully fail).

## Content

binder.proto - models used for binder interactions
backend_config.proto - models used for delivering quasmodrom config to clients
