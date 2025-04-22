# Status model

This section covers:

* Steps of the delivery claim processing.

* API methods that are available at specific steps of claim processing and let you change the claim status.

## Steps of order creation and execution {#process}

* At the [Order created](#create) step, a new claim is checked and evaluated, and the performer is searched for the order.

* If the order is created successfully, the driver arrives at the sender and [picks up the item](#pickup) to be delivered.

* After successful pickup, the performer [delivers the order](#delivery) to the specified addresses.

* If an item couldn't be delivered, the [item is returned](#return) to the return point.

At every step of creating and processing an order, you can [get information](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) about your claim. [Order change journal](https://yandex.com/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsJournal.html) lets you track the history of your claim.

![Order processing 1](https://yastatic.net/s3/doc-binary/src/dev/logistics/en/api/files/status-model-1-en.png)

![Order processing 2](https://yastatic.net/s3/doc-binary/src/dev/logistics/en/api/files/status-model-2-en.png)

<style>
    .doc-c-number-in-circle { width: 25px;
        height: 25px;
        line-height: 25px;
        -moz-border-radius: 50%;
        border-radius: 50%;
        background-color: #333333;
        color: #FFFFFF;
        text-align: center;
        display: inline-block; }
</style> 

## Order creation {#create}

<span class="number-in-circle">1</span> The request [Creating claims with multiple route points](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsCreate.html) initiates the order creation process.

<span class="number-in-circle">2</span> After the claim is created, the claim evaluation procedure starts. To find out the result of evaluation, run the request [Getting information on claims with multiple route points](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html).

<span class="number-in-circle">3</span> If the evaluation is successful, the claim switches to the awaiting confirmation status. The request for [getting information about the claim](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) returns the order cost for the client. If necessary, edit the claim by using the method [Editing a claim with multiple route points](https://yandex.com/dev/logistics/api/ref/claim-edit/IntegrationV2ClaimsEdit.html). After editing, the claim is automatically sent for evaluation. To confirm the claim, send the request [Confirm claim](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsAccept.html) within 10 minutes after the claim status switches to `ready_for_approval`.

<span class="number-in-circle">4</span> The claim could not be evaluated. The request for [getting information about the claim](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) returns the reasons why the claim couldn't be executed in the `error_messages` field. The claim can be sent for repeat evaluation after [editing](https://yandex.com/dev/logistics/api/ref/claim-edit/IntegrationV2ClaimsEdit.html).

<span class="number-in-circle">5</span> After the claim is confirmed, the performer search process starts.

<span class="number-in-circle">6</span> If you confirmed the claim 10 minutes or more after the claim status switched to `ready_for_approval`, the claim changes to the error status. Create a new claim in this case.

<span class="number-in-circle">7</span> The system searches for a performer based on the requirements you specified in your claim.

<span class="number-in-circle">8</span> The performer is selected for your claim.
From now until the order is completed you can request the following information:

* The data about the driver and vehicle: use the method [Getting information on claims with multiple route points](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) and look up the `performer_info` field in the response.

* Driver's phone number: use the method [Get phone number to call the driver](https://yandex.com/dev/logistics/api/ref/performer-info/IntegrationV1DriverVoiceForwarding.html). If the driver is replaced for any reason, request the phone number again.

* Coordinates of the current performer's location: use the method [Get claim performer position](https://yandex.com/dev/logistics/api/ref/performer-info/IntegrationV1ClaimsPerformerPosition.html).

<span class="number-in-circle">9</span> The performer was not found or canceled the order. Try creating a new claim.

{% note info "Note." %}

You can cancel your order for free at any step of order creation before the performer starts fulfilling it. To cancel your claim:

1. Make sure that you have access to free cancelation: the method [Getting information on claims with multiple route points](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html), the `available_cancel_state` field in the response.

2. Cancel the claim: use the method [Cancel claim](https://yandex.com/dev/logistics/api/ref/cancel-and-skip-points/IntegrationV2ClaimsCancel.html).

{% endnote %}

## Order pickup by driver {#pickup}

<span class="number-in-circle">10</span> The driver arrived at point A to pick up the order. After the driver reports to the system that they picked up the order, a confirmation code is generated automatically. The sender can get this code in their account profile, via SMS, or using the API [Get confirmation code](https://yandex.com/dev/logistics/api/ref/confirmation-code-and-acts/IntegrationV2ClaimsConfirmationCode.html) method.

<span class="number-in-circle">11</span> The driver waits for the sender to give the confirmation code.

<span class="number-in-circle">12</span> The driver entered the confirmation code into the system. Order acceptance by the driver is now confirmed. The request [Getting information on claims with multiple route points](https://yandex.com/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) returns information about a visit to the point in the `visit_status` field.

At steps 10 and 11, after the driver arrives for the order but before they receive it, you have the option to cancel the order for a fee using the [Cancel claim](https://yandex.com/dev/logistics/api/ref/cancel-and-skip-points/IntegrationV2ClaimsCancel.html) method.
At step 12, you can only cancel your order by contacting support. In this case, the driver has to return the item.

## Item delivery {#delivery}

<span class="number-in-circle">13</span> The driver arrived at point B to deliver the cargo to the recipient. When the driver reports to the system that they are ready to complete the order, the system generates a confirmation code and sends it to the recipient by SMS.

<span class="number-in-circle">14</span> The driver waits for the recipient to give the confirmation code.

<span class="number-in-circle">15</span> The driver entered the confirmation code into the system. Delivery to the recipient is now confirmed.
If the driver still has undelivered cargo, they proceed to the next recipient.

<span class="number-in-circle">16</span> All items are delivered to recipients.

<span class="number-in-circle">17</span> If at least one cargo unit can't be handed over to the recipient for some reason, such cargo is returned after the delivery is complete. By default, the return point is point A. If needed, you can specify a different return address.

At steps 13 and 14, before the cargo is handed over to the courier, you can cancel the order by contacting support. In this case, the driver has to return the cargo.

## Item return {#return}

<span class="number-in-circle">18</span> Driver arrived at the return point. After the driver reports to the system that they returned the order, a confirmation code is automatically generated. The sender can get this code in their account profile, via SMS, or using the API [Get confirmation code](https://yandex.com/dev/logistics/api/ref/confirmation-code-and-acts/IntegrationV2ClaimsConfirmationCode.html) method.

<span class="number-in-circle">19</span> The driver waits for the confirmation code.

<span class="number-in-circle">20</span> The driver entered the confirmation code into the system. Product return is now confirmed.

