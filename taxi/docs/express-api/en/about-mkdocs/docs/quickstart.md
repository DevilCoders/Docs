# Getting started

Before you start working with the Yandex Delivery API, [get](access.md) an OAuth token.

## Ordering transportation

Once you receive the token, you can use the Yandex Delivery API to order cargo transportation.

The ordering procedure is as follows:

1. Create a claim (use the operation [Creating claims with multiple route points](../ref/v2/claims/IntegrationV2ClaimsCreate-docpage)).<br/>
После попадания заявки в систему запустится процесс оценки заказа.
1. Find out the result of the order estimate (use the operation [Getting information on claims with multiple route points](../ref/v2/claims/IntegrationV2ClaimsInfo-docpage/)).<br/>
В случае успешной оценки вы получите стоимость для клиента.<br/>
Иначе ответ будет содержать причины, по которым заявка не может быть исполнена.
1. If necessary, edit the claim (use the operation [Editing a claim with multiple route points](../ref/v2/claims/IntegrationV2ClaimsEdit-docpage)).<br/>
До подтверждения заявки её можно редактировать.
1. Confirm the order (use the operation [Confirm claim](../ref/v1/claims/IntegrationV1ClaimsAccept-docpage)).<br/>
В случае успешной оценки заказ можно подтвердить, после чего запустится процесс поиска исполнителя.
1. Find out the status of the claim (use the operation [Get information on claims with multiple route points](../ref/v2/claims/IntegrationV2ClaimsInfo-docpage)).
1. If necessary, cancel the order (use the operation [Cancel claim](../ref/v1/claims/IntegrationV1ClaimsCancelC-docpage)).

