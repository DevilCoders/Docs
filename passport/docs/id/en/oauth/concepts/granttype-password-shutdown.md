# Disabling the ability to get a token by password

Applications registered in Yandex.OAuth after may 25, 2016 can't receive an OAuth token in exchange for the username and password (token requests with the `grant_type=password` parameter will be rejected). For other applications, this method of getting tokens was disabled on June 25, 2016.

This decision was made because this method of getting tokens recently didn't prove to be secure enough. Support often receives messages about the theft of personal information, bank card data, and other unpleasant situations.

Access to user data can be obtained only through the Yandex OAuth authorization form:

- [In a pop-up window](../reference/web-client.md).
    
- [In a new browser tab](../reference/auto-code-client.md).
    
- [In WebView](../reference/mobile-client.md) (for mobile apps).
    

