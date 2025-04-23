# Sender API Client
```go
senderClient := sender.NewHTTPClient(
    logger,
    sender.Config{
        HTTPClient:                &http.Client{Timeout: 1 * time.Second},
        AuthKey:                   "4d****************************28",
        SenderURL:                 "https://test.sender.yandex-team.ru",
        Account:                   "%account-slug%",
        AllowInactiveCampaigns:    true,
    },
)
```
## [Отправка транзакционных писем](https://github.yandex-team.ru/sendr/sendr/blob/master/docs/transaction-api.md)
- метод `SendTransactional`:
    ```go
    response, err := senderClient.SendTransactional(
    	context.Background(),
        &sender.TransactionalRequest{
            CampaignSlug: "1SLV2CV4-7D8",
            ToEmail:      "recipient@test.com",
            SendAsync:    true,
            Args:         map[string]string{"name": "username", "some_html": "<p style=\"color: red;\">some html is here</p>"},
        },
    )
    ```

## [Работа со списками отписок](https://github.yandex-team.ru/sendr/sendr/blob/master/docs/unsubscribe-api.md)
- метод `Unsubscribe`:
    ```go
    err := senderClient.Unsubscribe(
    	context.Background(),
        &sender.UnsubscribeListRequest{
            UnsubscribeListSlug: "1SLV2CV4-7D8",
            Email:      "recipient@test.com",
        },
    )
    ```
- метод `Subscribe`:
    ```go
    err := senderClient.Subscribe(
    	context.Background(),
        &sender.UnsubscribeListRequest{
            UnsubscribeListSlug: "1SLV2CV4-7D8",
            Email:      "recipient@test.com",
        },
    )
    ```
