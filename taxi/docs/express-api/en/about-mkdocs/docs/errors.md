# Errors 

|Error code | Error message | Description |
|:--- |:--- |:--- |
|401|unauthorized|Wrong token. Get correct token in your account.|
|500|Internal server error|Try again later or contact our support.|
|409|inappropriate_status|Action unavailable. Claim has been already confirmed or cancelled or you can’t perform this action on a claim.|
|400|Parse error|Check your JSON for errors.|
|400|unknown_zone|Wrong coordinates. Check the order: [longitude, latitude] and try to find your place on Yandex Maps.|
|400|invalid_destination_point|There’s a point but no parcels for it.|
|400|invalid_phone_must_start_plus_symbol|Wrong phone format. Check phone format. Example: `+13022461037`.|
|400|invalid_phone_size_incorrect|Wrong phone size. The size of your phone number must face your local requirements.|
|400|required_tariffs_disabled_for_user|Tariffs unavailable. The test account has expired or the specified tariff is not yet added to your account.|
|400|too_many_loaders|The maximum number of loaders is 2.|
|400|delay_too_long|The maximum number of days for `due` is 3.|
