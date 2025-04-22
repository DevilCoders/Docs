# Releases

The following is a list of changes to the API from version to version.

### Version 1.0.13 {#version-1-0-13}

**06.07.20**

- Added a new operation [Get confirmation code](../ref/v2/claims/IntegrationV2ClaimsConfirmationCode-docpage).

### Version 1.0.12 {#version-1-0-12}

**03.07.20**

- Corrected information about environments.

### Version 1.0.11 {#version-1-0-11}

**24.06.20**

- Added the `referral_source` field to specify the claim source.

### Version 1.0.10 {#version-1-0-10}

**19.06.20**

- Added new operations: [Get available classes](../ref/v1/estimate/IntegrationV1Tariffs-docpage) and [Estimate claim and vehicle parameters without creating an offer](../ref/v1/estimate/IntegrationV1CheckPrice-docpage).

### Version 1.0.9 {#version-1-0-9}

**10.06.20**

- Added a field with the client's order number on the point `external_order_id` when creating a claim.

### Version 1.0.8 {#version-1-0-8}

**21.05.20**

- Added the status `failed`.

- Added the indicator `resolution` in the journal for terminal statuses.

### Version 1.0.7 {#version-1-0-7}

**12.05.20**

- Added information about the position of the order performer.

### Version 1.0.6 {#version-1-0-6}

**27.04.20**

- Added the phone number of the order performer.

- Added a list of errors when creating a claim.

- Added a list of warnings when creating a claim.

### Version 1.0.5 {#version-1-0-5}

**23.04.20**

- The Notification mechanism for status changes is deprecated, and the journal should be used instead.

### Version 1.0.4 {#version-1-0-4}

**21.04.20**

- Added information about payment upon receipt.

- Added a field for general comments related to the order (comment in the claim root).

- Added the option to refuse delivery to the door (see `skip_door_to_door`).

### Version 1.0.3 {#version-1-0-3}

**21.04.20**

- Added the order change journal API.

### Version 1.0.2 {#version-1-0-2}

**11.04.20**

- Added order API with multiple route points.

- Fixed the token lifetime description – now it is unlimited.

- Added an operation to get information on multiple claims `v2/bulk_info`.

## Version 1.0.1 {#version-1-0-1}

**07.04.20**

- Added description of claim statuses.

- Added notification section for claim status changes.

- Added the ability to not send automatic notifications to the sender/recipient (see `skip_client_notify`).

- Added the ability to create an order without the need to return the items in case of cancelation of the order (the courier keeps the items) (see `optional_return`).

- Added the ability to create an order for a specific time (no later than 36 hours) (see `due`).

- Added currency to the taxi offer price (see `pricing`).

- Added the final price of the order (including cancelations, paid waiting, and so on) (see `pricing`).

- Added the ability for the client to choose the size of the vehicle (without vehicle size guarantees).

