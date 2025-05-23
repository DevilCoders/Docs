# Payment

This block lets users transfer money to a wallet in the YooMoney payment system (previously, Yandex.Money). For example, as payment for attending an event.

From the **Payment** block, the user is redirected to the company's website [ЮMoney]({{ link-yoomoney }}) to complete the payment. {{ forms-full-name }} only register the user's transition to the payment page. You can get information about payments and fees from YooMoney.

{% note warning %}

You can only use the **Payment** block to accept payments to a registered or identified wallet belonging to an individual. The transfer fee is deducted from the recipient.

{% endnote %}

## Block settings {#sec_settings}

### Question {#param-question}

Enter the payment field name. For example, state the purpose of the payment.

{% include [question](../../_includes/forms/question.md) %}

{% include [id-required-hidden](../../_includes/forms/id-required-hidden.md) %}

### Amount {#param-sum}

Specify the payment amount.

### Fixed amount {#param-sum-static}

Turn this option on so the user can't change the payment amount.

### Recipient's wallet number {#param-wallet-in}

Specify the number of the YooMoney wallet you will use to accept payments.

