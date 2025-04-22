# Интерфейс договора Биллинга

### Реализация интерфейса для dict-like представления JSONContract

Пример:
```(python)
>>> contract = JSONContract(contract_data={
    "client_id": 86933666,
    "collaterals": {
        "0": {
            "attribute_batch_id": 11998541,
            "collateral_type_id": null,
            "contract2_id": 1666674,
            "contract_type": 9,
            "create_dt": "2020-06-13T00:04:55",
            "currency": 840,
            "doc_set": null,
            "dt": "2020-06-12T00:00:00",
            "firm": 7,
            "id": 2066011,
            "is_cancelled": null,
            "is_faxed": null,
            "is_signed": null,
            "market_api_pct": "50",
            "memo": "Договор создан автоматически\n",
            "nds": 0,
            "num": null,
            "open_date": 0,
            "partner_pct": "43",
            "passport_id": 5166666840,
            "pay_to": 1,
            "payment_type": 1,
            "print_tpl_barcode": 99966668845,
            "reward_type": 1,
            "search_forms": 1,
            "service_start_dt": "2020-06-12T00:00:00",
            "services": {
                "290": 1
            },
            "test_mode": 1,
            "unilateral_acts": 0,
            "update_dt": "2020-06-13T00:04:55"
        }
    },
    "extprops": {
        "is_process_taxi_netting_in_oebs_": {
            "_meta": {
                "values_native_type": null,
                "data_column": "value_num",
                "native_type": "bool"
            },
            "value": false
        },
        "cpf_netting_last_dt": {
            "_meta": {
                "values_native_type": null,
                "data_column": "value_dt",
                "native_type": null
            },
            "value": null
        },
        "offer_accepted": {
            "_meta": {
                "values_native_type": null,
                "data_column": "value_num",
                "native_type": "bool"
            },
            "value": true
        },
        "daily_state": {
            "_meta": {
                "values_native_type": null,
                "data_column": "value_dt",
                "native_type": null
            },
            "value": null
        },
        "service_code": {
            "_meta": {
                "values_native_type": null,
                "data_column": "value_str",
                "native_type": null
            },
            "value": null
        }
    },
    "external_id": "YAN-16664-06/20",
    "id": 1681374,
    "passport_id": 5166666840,
    "person_id": 1066678,
    "type": "PARTNERS",
    "update_dt": "2020-06-13T00:04:55",
    "version_id": 0
}

>>> contract.client_id
86933666
```
