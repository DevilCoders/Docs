# Hubs

All the actual styles for all the things are placed here.

Each hub can be loaded independently, and there could be sub-hubs.

Current hubs:

- `boot`, contains all the styles that should be there while the Mail is loading. They can share some of the common styles that are used for the blocks that are common both for the boot part and the app part.

- `common` contains all the common stuff that can be used everywhere, with the exception for those things that should be there at the `boot` stage. All the global modifiers like `is-hidden`, all the common abstract ui-stuff like `ui-grid` are placed there.

- `mail` contains all the stuff that is used for Mail app, contains sub-hubs.
