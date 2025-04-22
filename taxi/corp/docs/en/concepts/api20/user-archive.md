# Archive a user

This request is used to archive a client's user. When archived, the user disappears from the account profile. The user can't use the services and can't be found in the account profile.

If you try to create a user with the same phone number as the archived user, an error will occur. In this case, instead of creating a new user, you must [restore the user from the archive](#restore) with updated data.

{% note info %}

We strongly recommend not changing the user's phone number. Instead, [create a new user](user-create.md).

{% endnote %}


## Request syntax

```
GET https://b2b-api.go.yandex.ru/integration/2.0/users/{user ID}/archive
```

**Request headers**

#### Authorization
OAuth access token. The steps to get a token are described in [Getting started](../quickstart.md).

## Response field description

The response contains the following fields:

Field | Description | Format
----- | ----- | -----
`id` | The user's ID number. | String


## Request example

```
GET https://b2b-api.go.yandex.ru/integration/2.0/users/f65...c57d/archive
...
Authorization: Bearer <OAuth token>
```

## Response example

An example response to this request looks like this:

```no-highlight
{
        "id": "3caa3587675b49deb62e3286b753b05e"
}
```

## Response codes

The response to this request may contain the following standard HTTP codes:

- `200`: Request completed successfully.
- `401`: The [OAuth token](../quickstart.md) is incorrect.
- `403`: The client doesn't have sufficient rights to execute this request.
- `404`: The requested record wasn't found.


## Restore an archived user {#restore}

To restore a user, you need to send a request to [edit a user](user-update.md) and add the `is_deleted: false` flag.

