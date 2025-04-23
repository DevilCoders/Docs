# Steps for logging in via Yandex

General steps for using Yandex to authenticate a user on your website:

1. On the website, a Yandex user clicks a button to log in via Yandex. 

   The website [connected to the Yandex ID API](../concepts/adoption.md), redirects the user to [Yandex.OAuth]{% if lang == "en" %}(https://oauth.yandex.com){% endif %} and requests access to specific account data on Yandex.

1. The user grants access to personal data.
   
   The website [gets an OAuth access token](../../oauth/reference/web-client.md) that grants permission to request this user's email addresses.
   
1. The website sends a [request to the Yandex ID API](../reference/request.md) specifying the obtained token.

   The website receives the user's unique ID and the list of email addresses. The response format is described in [Response format and content](../reference/response.md).

   {% note info "Note" %}

   To send a request to the Yandex ID API, you may use an OAuth token with permissions to access any of the Yandex services (Yandex.Fotki, Yandex.Disk, and other services). However, extended access to user data is only available if you have tokens with permissions from the **Yandex ID API** section.

   {% endnote %}

1. 	The site authenticates the user, using the content and settings that are assigned to this ID.

This enables a Yandex user to obtain an account on a website and get authenticated on the site, without having to create a new account.