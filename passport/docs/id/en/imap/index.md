# OAuth authorization in Yandex.Mail

Mail clients and applications can access Yandex.Mail mailboxes using the OAuth protocol. With this protocol, programs don't request or store usernames and passwords, and users don't have to worry about password security.

OAuth authorization is supported by Yandex.Mail IMAP and SMTP servers. Authorization is implemented using the XOAUTH2 mechanism, which is also used by [Gmail](https://developers.google.com/gmail/xoauth2_protocol).


## Connection {#quickstart}

To implement OAuth authorization in your mail client:

1. [Register the application](../oauth/tasks/register-client.md) on Yandex.OAuth with the following rights:
    
    - For authentication on the SMTP server: .
    
    - For authentication on the IMAP server:  or **Reading and deleting messages in Yandex.Mail**.
    
1. Implement the request for OAuth tokens using any available method (see the [Yandex.OAuth documentation](../oauth/concepts/about.md)). You can use the [debug token](../oauth/tasks/get-oauth-token.md) for initial testing.
    
1. Set up sending OAuth tokens to Yandex.Mail and server response processing. Proper communication with Yandex.Mail servers over the [IMAP](#imap) and [SMTP](#smtp) protocols is described below.
    

### Mail server addresses {#quickstart}

Mail servers should be accessed at the following addresses:

- IMAP server: `imap.yandex.com:993`.
    
- SMTP server: `smtp.yandex.com:465`.
    


## Communication with the IMAP server {#imap}

When authenticating on the IMAP server, your program must use the `AUTHENTICATE` command with the `XOAUTH2` mechanism (the mechanism is supported, although it is not mentioned in the `CAPABILITY` command output). The user's OAuth token and email should be passed in the command argument.

To create an argument with authorization data:

1. Prepare the data string:
    
    ```no-highlight
    user=<login>\@yandex.com\001auth=Bearer <OAuth-token>\001\001
    ```
    
1. Encode the resulting string using the base64 method, for example:
    
    ```no-highlight
    dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
    ```
    

The `AUTHENTICATE` command should be formatted as a single string without breaks or hyphens (the example below is formatted to make it easier to read). If the IMAP authentication is successful, the sequence of requests and responses may look like this:

```no-highlight
openssl s_client -connect imap.yandex.com:993 -crlf

<connection initialization>

client: C01 CAPABILITY
server: * CAPABILITY IMAP4rev1 CHILDREN UNSELECT LITERAL+ NAMESPACE XLIST BINARY UIDPLUS ENABLE ID AUTH=PLAIN IDLE MOVE
server: C01 OK CAPABILITY Completed.
client: A01 AUTHENTICATE XOAUTH2 dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
server: * CAPABILITY IMAP4rev1 CHILDREN UNSELECT LITERAL+ NAMESPACE XLIST BINARY UIDPLUS ENABLE ID IDLE MOVE
server: A01 OK AUTHENTICATE Completed.

<continue work>
```

### Authentication error response {#imap}

The server returns an error description in response to the `AUTHENTICATE` command. If there is an IMAP authentication error, the sequence of requests and responses may look like this:

```no-highlight
openssl s_client -connect imap.yandex.com:993 -crlf

<connection initialization>

client: C01 CAPABILITY
server: * CAPABILITY CHILDREN UNSELECT LITERAL+ NAMESPACE XLIST BINARY UIDPLUS ENABLE ID AUTH=PLAIN IDLE MOVE
server: C01 OK CAPABILITY Completed.
client: A01 AUTHENTICATE XOAUTH2 dXNlcj10ZXN0MUB5YW5kZXgucnUBYXV0aD1CZWFyZXIgQXJkRmZpZ0FBS0Z3RVVicFpxMUZReHVmd0pscnEtcEUyZwEB
server: A01 NO [AUTHENTICATIONFAILED] AUTHENTICATE Invalid credentials or IMAP is disabled sc=ANQhQk2BrGkH_101523_7m

<continue work>
```
After the error description, the server provides a sequence of the `sc=ANQrQk2BrGkH_101523_7m` type. This is the session ID you should specify when contacting the Yandex.Mail support service about this error.

## Communication with the SMTP server {#smtp}

When authenticating on the SMTP server, your program must use the `AUTH` command with the `XOAUTH2` mechanism. The user's token and login should be encoded and passed in the command argument.

The argument with authorization data is created in the same way as for the IMAP protocol:

1. Prepare the data string:
    
    ```no-highlight
    user=<login>\@yandex.com\001auth=Bearer <OAuth-token>\001\001
    ```
    
1. Encode the resulting string using the base64 method, for example:
    
    ```no-highlight
    dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
    ```
    

If the SMTP authentication is successful, the sequence of requests and responses looks like this:

```no-highlight
openssl s_client -connect smtp.yandex.com:465 -crlf

<connection initialization>

server: 220 smtp2o.mail.yandex.net ESMTP (Want to use Yandex.Mail for your domain? Visit http://pdd.yandex.ru)
client:EHLO sender.example.com
server:250-smtp2o.mail.yandex.net
server:250-8BITMIME
server:250-PIPELINING server:250-SIZE 42991616
server:250-AUTH LOGIN PLAIN XOAUTH2
server:250-DSN
server:250 ENHANCEDSTATUSCODES
client:AUTH XOAUTH2 dXNlcj10ZXN0QHlhbmRleC5ydQFhdXRoPUJlYXJlciBBcmRGZmlnQUFLRndFVWJwWnExRlF4dWZ3SmxycS1wRTJnAQE=
server:235 2.7.0 Authentication successful.

<continue work>
```

The `AUTH` command should be formatted as a single string without breaks (the example below is formatted to make it easier to read).

### Authentication error response {#smtp}

The server returns an error description in response to the `AUTH` command, with code 535.

Example of a request–response sequence for an SMTP authentication error:

```no-highlight
openssl s_client -connect smtp.yandex.com:465 -crlf

<connection initialization>

server: 220 smtp2o.mail.yandex.net ESMTP (Want to use Yandex.Mail for your domain? Visit http://pdd.yandex.ru)
client:EHLO sender.example.com
server:250-smtp2o.mail.yandex.net
server:250-8BITMIME
server:250-PIPELINING
server:250-SIZE 42991616
server:250-AUTH LOGIN PLAIN XOAUTH2
server:250-DSN
server:250 ENHANCEDSTATUSCODES
client:AUTH XOAUTH2 dXNlcj10ZXN0MUB5YW5kZXgucnUBYXV0aD1CZWFyZXIgQXJkRmZpZ0FBS0Z3RVVicFpxMUZReHVmd0pscnEtcEUyZwEB
server:535 5.7.8 Error: authentication failed: Invalid user or password!

<continue work>
```

If the authentication string was incorrect, the error will be as follows:

```no-highlight
server: 535 5.7.8 Error: authentication failed:Invalid format.
```

