# About
This is a tool to add mappings (quota request resource -> resources model resource) to Dispenser.

Supported parameters are:
````
resource-mapping-tool --file data.json
    --dry-run
    -e, --env (prod|test)

````

Format for input file:
````json
[
    {
        "campaignId": 42,
        "mappings": [
            {
                "serviceKey": "<dispenser provider key>",
                "resourceKey": "<dispenser resource key>",
                "segmentKeys": ["<dispenser segment keys>"],
                "targets": [
                    {
                        "externalProviderKey": "<d provider key>",
                        "externalResourceKey": "<d resource key>",
                        "externalUnitKey": "<d resource unit key>",
                        "key": "optional <dispenser key for mapping>",
                        "numerator": 1,
                        "denominator": 1
                    }
                ]
            },
            {
                "serviceKey": "<dispenser provider key>",
                "resourceKey": "<dispenser resource key>",
                "segmentKeys": ["<dispenser segment keys>"],
                "targets": []
            }
        ]
    }
]
````

How to install:
- Setup Arcadia using this [guide](https://docs.yandex-team.ru/devtools/).
- Execute ``ya make`` in ``${ARCADIA_ROOT}/intranet/dispenser/utils/resource-mapping-tool``
- SSH key needs to be registered on Staff, this key is required to get an OAuth token
- Run the tool
