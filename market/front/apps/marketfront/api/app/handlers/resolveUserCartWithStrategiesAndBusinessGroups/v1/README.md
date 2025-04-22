# Резолвер resolveUserCartWithStrategiesAndBusinessGroups

Резолвер для получения бизнес-групп для отображения их в корзине. Используется только на мобильных устройствах.

\* - Обязательный параметр

## Параметры из тела запроса

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `enableMultiOffers` | boolean |  | - |
| `showUrls` | boolean |  | - |
| `filterExpiredCart` | boolean | Нужно ли вырезать бакет с протухшими товарами  | - |
| `filterExpiredCart` | boolean |  | - |
| `regset` | number |  | - |
| `rgb` | Rgb |  | RGB.BLUE |
| `dsbsEnabled` | boolean |  | false |
| `showDigitalDsbsGoods` | boolean | Показывать ли в выдаче цифровые товары. Для мобилок по умолчанию не показываем | false |
| `enableNonMskuDsbsOffers` | boolean | Готовность получать dsbs офферы без msku | false |
| `showPreorder` | boolean | Готовность получать предзаказные оферы | false |
| `cpa` | CpaValue |  | - |
| `splitStrategy` | string | Разделение по посылкам: медицина и обычные товары. | - |
| `cartItems` | CartItem[] | Массив элементов корзины. Если передан, вместо похода в картер используем данный параметр. | - |


## Пример запроса

```
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveUserCartWithStrategiesAndBusinessGroups' \
--data-raw '{
	"params": [{}]
}'
```

## Пример ответа

```json
{
  "results": [
    {
      "handler": "resolveUserCartWithStrategiesAndBusinessGroups",
      "result": {
        "strategyIds": [
          "consolidate-without-crossdock"
        ],
        "cartBusinessGroupIds": [
          "2_DEFAULT"
        ]
      }
    }
  ],
  "collections": {
    "combineStrategy": [
      {
        "name": "consolidate-without-crossdock",
        "default": true,
        "carts": [
          {
            "warehouseId": 48339,
            "shopId": 10671634,
            "isFulfillment": false,
            "isDigital": false,
            "hasCourier": false,
            "hasPickup": true,
            "hasOnDemand": false,
            "isPartialDeliveryAvailable": false,
            "IsEdaParcel": false,
            "IsExpressParcel": false,
            "wasSplitByCombinator": false,
            "deliveryDayFrom": 4,
            "offers": [
              {
                "wareId": "LcxYZnQeCoXqTnEmyeCq1w",
                "replacedId": "LcxYZnQeCoXqTnEmyeCq1w",
                "count": 1,
                "cartItemIds": [
                  1635848933221
                ]
              }
            ],
            "overcomeRestrictionsForReplacement": [],
            "currentRestrictionsForReplacement": [],
            "deliveryPartnerTypes": [
              "YANDEX_MARKET"
            ]
          }
        ],
        "id": "consolidate-without-crossdock",
        "automaticReplacement": true,
        "hasOvercomeRestrictions": false,
        "priceHasChanged": false
      }
    ],
    "offerShowPlace": [
      {
        "id": "THi2k-pxPNJcs24AmweTv2akn_hY-WuBUO5nXTQPOnwT8gFokXxATRdeqknkMUgi1Y7BBbDXNWfiKq714ZyHxqiPLOcKBWGxyZtIcXM8E32uFEKUvVkTbMiKLiuoXl5HvQFFzgjGS2C8f8G8dT6Wsk_eEjZolppz2oXB-pv578c,",
        "offerId": "LcxYZnQeCoXqTnEmyeCq1w",
        "entity": "offerShowPlace",
        "feeShow": "THi2k-pxPNJcs24AmweTv2akn_hY-WuBUO5nXTQPOnwT8gFokXxATRdeqknkMUgi1Y7BBbDXNWfiKq714ZyHxqiPLOcKBWGxyZtIcXM8E32uFEKUvVkTbMiKLiuoXl5HvQFFzgjGS2C8f8G8dT6Wsk_eEjZolppz2oXB-pv578c,",
        "showUid": "16358937753910035464206000",
        "urls": {
          "cpa": "/safeclick/data=338FT8NBgRsBwTfDX0JTTL9-Vq8E-EqVjXqfY9n1OBv3uPh67uaAoT-iTEhVZbl7o5IACN0RtBvcd2H9_dkK5jYpUgyHsL0uPVwSERMa1ouPZuuMEHgagBDW0902I0Hhgau95NCy2bF5J1DW-t9EeL5RpE5EgLkAHnpl7OpCJ6pp_qQuOVK0kipAKWgr77OZajEGUTtSmWF2ve9-XUj7XklZ1U_bvrXsT33YPf6TkGZ-7kz6uV9zpwSmzNGRiR2GrQ8KEiGj7O6tluHoozowOsqIO1SyZlNwgjx7XsR7zYFO3j_VpZ0gnpdtFt8QPQ_On8ow96uNBFDh3IS71B9OIIZynE59j4mFRTVVcPmzPlR61GA7wJxFvT_nxD2l6S0RaFww1d2VXlOnJdtIbZep71cxnJHMoSXZzdihtILSZ4lkh7Vp1Fdibikvc4wMTTiXlWDRrjCSagDDPlbIbTPpP81ae9mc90H0XuDxQs4EHCOFAroh8Lv9Fm7AeGYHqbRa45327ePvgA78p0LSocT52U6XHD1rLTrK0dT1iehWDi9dohjpCXx2Uphojx4hyUPU_nuQ7bsQMFEWt7bMkjr0eXA5P2R8I6i0L94qMTxHfMATBnEfiLW9kUp5UhAbeUfiG5pzcik3reQ8XmBgpFZENsg7yL55rCgT2sM7l2dN3T-cW6e0jFIZQ67zI3BfsUKNJJnG8R2Ay1ArcyK5zeU2db5GBwFilMBfbYzWMz8vOKR0u0d9gpDk0Esia5RVNsp54jXo-NhSUfe1WpkiPAkKBV_Mac754Eh4bLAFdL2NXGnZecRgbDWKvv5R0vm8fHrHGOVt6qkrpDMwgBbYrhu0xcSVlqrimh1o2n7hY2P3WBHHx9uIFU9tNAevBDPa-HUEg0kglNbPqMO0jte8NY7Nld3y6q0VdupS8bFN2VMB2lP9guSBCnk8HpFwGhnR9-AnvA5_T9ioMIPVfbtDZUI5RN8uaNVYaxrN_1SXETYkeDzgoB0TX2UU8e5z6IjM1tOqhL5Denp3VmQ0VAdPzFOvoiO2Zw7b7WkuEfewdzm1KJ0__2kduTrSfihCh9NfwZAF0SHCK6cKNGiG4y3kFUJ1ovj_x7bKZo122GW479MIr35IjIR4PwTnprBVFY5O32BbRc8E4I9UKxGJpxxaMIe2mHApN3p8UyfYSICk_UfyeZGYGklzd_rpBOQj4UmZ1YksZIZUKbP8LlEuit8Qv7g1ZUlwDWri79YL/b64e=1/sign=b2506aa125c696404fe7d1209a3a0817/keyno=1/*",
          "direct": "https://pokupki.market.yandex.ru/product/100131945690?offerid=LcxYZnQeCoXqTnEmyeCq1w&cpc=ZS2RhJcSEPXNog7h0IISiutg70w0aqSg2E-ODX_phOh22Cluc911GMDbnX18BwBcNrFfVQAZ-TwOMwdZof1WzLGs8uEbCcrnGBFOC1dfZM2Zek4eYAuks6MNlHxwto2rVQzncZdM_Ip9fPGVHIA_hN9NtJZlfYozmLwU4gTYcqA,"
        },
        "cpc": "ZS2RhJcSEPXNog7h0IISiutg70w0aqSg2E-ODX_phOh22Cluc911GMDbnX18BwBcNrFfVQAZ-TwOMwdZof1WzLGs8uEbCcrnGBFOC1dfZM2Zek4eYAuks6MNlHxwto2rVQzncZdM_Ip9fPGVHIA_hN9NtJZlfYozmLwU4gTYcqA,",
        "promoIds": []
      }
    ],
    "offer": [
      {
        "categoryIds": [
          91491
        ],
        "shopId": 10671634,
        "supplierId": 10671634,
        "navnodeIds": [
          26893750
        ],
        "vendorId": 7701962,
        "warehouseId": 48339,
        "fulfillmentWarehouseId": 100136,
        "price": {
          "value": 9999,
          "currency": "RUR"
        },
        "discount": {
          "currentPrice": {
            "value": 9999,
            "currency": "RUR"
          }
        },
        "promos": [],
        "dimensions": {
          "width": 20,
          "height": 20,
          "depth": 20
        },
        "weight": 1100,
        "id": "LcxYZnQeCoXqTnEmyeCq1w",
        "feed": {
          "id": 200720578,
          "offerId": "hid.100131945690"
        },
        "isPreorder": false,
        "isFulfilment": false,
        "isFashion": false,
        "isFashionPremium": false,
        "isPartialCheckoutAvailable": false,
        "availableCount": 235,
        "isDefault": false,
        "productId": 1720465387,
        "delivery": {
          "courierOptions": [],
          "isCourierAvailable": false,
          "partnerTypes": [
            "YANDEX_MARKET"
          ],
          "isBetterWithPlus": true,
          "isFree": false,
          "hasPost": true,
          "hasPickup": true,
          "inStock": false,
          "isDownloadable": false,
          "isPriorityRegion": false,
          "hasLocalStore": true,
          "shopPriorityCountry": 225,
          "shopPriorityRegion": 2,
          "postStats": {
            "minDays": 3,
            "maxDays": 4,
            "minPrice": {
              "value": 49,
              "currency": "RUR"
            },
            "maxPrice": {
              "value": 49,
              "currency": "RUR"
            }
          },
          "isExpress": false,
          "isEda": false,
          "options": []
        },
        "creditInfo": {
          "termRange": {
            "min": 24,
            "max": 24
          },
          "bestOptionId": "1",
          "initialPayment": {
            "currency": "RUR",
            "value": "0"
          },
          "monthlyPayment": {
            "currency": "RUR",
            "value": "526"
          }
        },
        "skuCreator": "market",
        "bnplAvailable": false,
        "financialProductPriority": [
          "TINKOFF_CREDIT"
        ],
        "isCashbackSpendAvailable": true,
        "businessId": 10728534,
        "wareId": "LcxYZnQeCoXqTnEmyeCq1w",
        "entity": "offer",
        "marketSku": "100131945690",
        "prepayEnabled": false,
        "bundleSettings": {
          "quantityLimit": {
            "minimum": 1,
            "step": 1
          }
        },
        "cpa": "real",
        "description": "",
        "meta": {},
        "modelAwareTitles": {
          "raw": "Смартфон Xiaomi Redmi 4X 32GB, черный",
          "highlighted": [
            {
              "value": "Смартфон Xiaomi Redmi 4X 32GB, черный"
            }
          ]
        },
        "pictures": [
          {
            "entity": "picture",
            "original": {
              "width": 218,
              "height": 411,
              "namespace": "mpic",
              "groupId": 96484,
              "key": "img_id7306727891630419427"
            },
          },
          {
            "entity": "picture",
            "original": {
              "width": 220,
              "height": 408,
              "namespace": "mpic",
              "groupId": 200316,
              "key": "img_id2847787433556056781"
            },
          },
          {
            "entity": "picture",
            "original": {
              "width": 42,
              "height": 397,
              "namespace": "mpic",
              "groupId": 96484,
              "key": "img_id2914588490470205083"
            },
          }
        ],
        "promoCodeEnabled": true,
        "seller": {
          "price": "9999",
          "currency": "RUR",
          "sellerToUserExchangeRate": 1
        },
        "shopSku": "hid.100131945690",
        "titles": {
          "raw": "Смартфон Xiaomi Redmi 4X 32GB, черный",
          "highlighted": [
            {
              "value": "Смартфон Xiaomi Redmi 4X 32GB, черный"
            }
          ]
        },
        "slug": "smartfon-xiaomi-redmi-4x-32gb-chernyi",
        "manufacturer": {
          "entity": "manufacturer",
          "warranty": false,
          "country": "Россия",
          "countries": [
            {
              "entity": "region",
              "id": 225,
              "name": "Россия",
              "lingua": {
                "name": {
                  "genitive": "России",
                  "preposition": "в",
                  "prepositional": "России",
                  "accusative": "Россию"
                }
              },
              "type": 3
            }
          ]
        },
        "cargoTypes": [
          200,
          980
        ],
        "atSupplierWarehouse": true,
        "offerColor": "blue",
        "restrictedAge18": false,
        "specs": {
          "internal": []
        },
        "prices": {
          "currency": "RUR",
          "value": "9999",
          "isDeliveryIncluded": false,
          "isPickupIncluded": false,
          "rawValue": "9999"
        },
        "payments": {
          "deliveryCard": false,
          "deliveryCash": false,
          "prepaymentCard": false,
          "prepaymentOther": false
        }
      }
    ],
    "shop": [
      {
        "id": 10671634,
        "name": "Дропшип под нагрузку скрытий",
        "shopName": "Дропшип под нагрузку скрытий",
        "feedId": "200720578",
        "loyaltyProgramStatus": "ENABLED",
        "entity": "shop",
        "slug": "dropship-pod-nagruzku-skrytii",
        "cutoff": "",
        "gradesCount": 1,
        "overallGradesCount": 1,
        "bookNowStoresCount": 0,
        "status": "",
        "storesCount": 0,
        "qualityRating": 0,
        "newGradesCount3M": 1,
        "newGradesCount": 1,
        "isGlobal": false,
        "subsidies": true,
        "ratingToShow": 0,
        "outletsCount": 0,
        "ratingType": 6,
        "business_id": 10728534,
        "business_name": "Дропшип под нагрузку скрытий",
        "operationalRatingId": 10671634
      }
    ],
    "operationalRating": [
      {
        "id": 10671634,
        "entity": "operationalRating",
        "viewType": "AS_IS",
        "lateShipRate": 0,
        "lateShipRateMark": 1,
        "lateShipRateOperationalRatingLevel": "LOW",
        "cancellationRate": 15,
        "cancellationRateMark": 1,
        "cancellationRateOperationalRatingLevel": "LOW",
        "returnRate": 100,
        "returnRateMark": 5,
        "returnRateOperationalRatingLevel": "HIGH",
        "total": 0,
        "totalMark": 1,
        "totalOperationalRatingLevel": "LOW",
        "crossdockPlanFactRate": 100,
        "crossdockPlanFactRateMark": 5,
        "crossdockOperationRatingLevel": "HIGH",
        "fulfillmentPlanFactRate": 100,
        "fulfillmentPlanFactRateMark": 5,
        "fulfillmentOperationRatingLevel": "HIGH"
      }
    ],
    "navnode": [
      {
        "id": 3938,
        "isDepartment": false,
        "pictures": []
      },
      {
        "id": 26893750,
        "isDepartment": false,
        "pictures": [],
        "entity": "navnode",
        "name": "Смартфоны",
        "fullName": "Смартфоны",
        "isLeaf": true,
        "slug": "smartfony-vo-vladimire",
        "rootNavnode": 3938
      }
    ],
    "category": [
      {
        "entity": "category",
        "id": 91491,
        "nid": 26893750,
        "name": "Мобильные телефоны",
        "slug": "mobilnye-telefony-vo-vladimire",
        "fullName": "Мобильные телефоны",
        "type": "guru",
        "cpaType": "cpc_and_cpa",
        "isLeaf": true,
        "kinds": []
      }
    ],
    "navnodePicture": [],
    "vendor": [
      {
        "logo": {
          "entity": "picture",
          "url": "//avatars.mds.yandex.net/get-mpic/1862933/img_id5477847296568171778.png/orig",
          "thumbnails": []
        },
        "id": 7701962,
        "slug": "xiaomi",
        "entity": "vendor",
        "filter": "7893318:7701962",
        "name": "Xiaomi",
        "website": "https://www.mi.com/ru"
      }
    ],
    "outlet": [],
    "organizationLegalInfo": [],
    "region": [
      {
        "entity": "region",
        "id": 2,
        "name": "Санкт-Петербург",
        "subtitle": "Санкт-Петербург и Ленинградская область, Россия",
        "type": "CITY",
        "linguistics": {
          "prepositional": "Санкт-Петербурге",
          "preposition": "в",
          "accusative": "Санкт-Петербург"
        }
      },
      {
        "entity": "region",
        "id": 225,
        "name": "Россия",
        "type": "CITY",
        "linguistics": {
          "prepositional": "России",
          "preposition": "в",
          "accusative": "Россию"
        }
      }
    ],
    "offerService": [],
    "product": [],
    "review": [],
    "ratingFactor": [],
    "aggregatePromo": [],
    "filter": [],
    "filterValue": [],
    "filterToValues": [],
    "benefit": [],
    "promo": [],
    "knownThumbnail": [
      {
        "id": "marketpic",
        "thumbnailIds": [
          "50x50",
          "55x70",
          "60x80",
          "74x100",
          "75x75",
          "90x120",
          "100x100",
          "120x160",
          "150x150",
          "180x240",
          "190x250",
          "200x200",
          "240x320",
          "300x300",
          "300x400",
          "600x600",
          "600x800",
          "900x1200",
          "x124_trim",
          "x166_trim",
          "x248_trim",
          "x332_trim"
        ]
      },
      {
        "id": "mpic",
        "thumbnailIds": [
          "1hq",
          "2hq",
          "3hq",
          "4hq",
          "5hq",
          "6hq",
          "7hq",
          "8hq",
          "9hq",
          "x124_trim",
          "x166_trim",
          "x248_trim",
          "x332_trim"
        ]
      }
    ],
    "thumbnail": [
      {
        "id": "50x50",
        "width": 50,
        "height": 50
      },
      {
        "id": "55x70",
        "width": 55,
        "height": 70
      },
      {
        "id": "60x80",
        "width": 60,
        "height": 80
      },
      {
        "id": "74x100",
        "width": 74,
        "height": 100
      },
      {
        "id": "75x75",
        "width": 75,
        "height": 75
      },
      {
        "id": "90x120",
        "width": 90,
        "height": 120
      },
      {
        "id": "100x100",
        "width": 100,
        "height": 100
      },
      {
        "id": "120x160",
        "width": 120,
        "height": 160
      },
      {
        "id": "150x150",
        "width": 150,
        "height": 150
      },
      {
        "id": "180x240",
        "width": 180,
        "height": 240
      },
      {
        "id": "190x250",
        "width": 190,
        "height": 250
      },
      {
        "id": "200x200",
        "width": 200,
        "height": 200
      },
      {
        "id": "240x320",
        "width": 240,
        "height": 320
      },
      {
        "id": "300x300",
        "width": 300,
        "height": 300
      },
      {
        "id": "300x400",
        "width": 300,
        "height": 400
      },
      {
        "id": "600x600",
        "width": 600,
        "height": 600
      },
      {
        "id": "600x800",
        "width": 600,
        "height": 800
      },
      {
        "id": "900x1200",
        "width": 900,
        "height": 1200
      },
      {
        "id": "x124_trim",
        "width": 166,
        "height": 124
      },
      {
        "id": "x166_trim",
        "width": 248,
        "height": 166
      },
      {
        "id": "x248_trim",
        "width": 332,
        "height": 248
      },
      {
        "id": "x332_trim",
        "width": 496,
        "height": 332
      },
      {
        "id": "1hq",
        "width": 50,
        "height": 50
      },
      {
        "id": "2hq",
        "width": 100,
        "height": 100
      },
      {
        "id": "3hq",
        "width": 75,
        "height": 75
      },
      {
        "id": "4hq",
        "width": 150,
        "height": 150
      },
      {
        "id": "5hq",
        "width": 200,
        "height": 200
      },
      {
        "id": "6hq",
        "width": 250,
        "height": 250
      },
      {
        "id": "7hq",
        "width": 120,
        "height": 120
      },
      {
        "id": "8hq",
        "width": 240,
        "height": 240
      },
      {
        "id": "9hq",
        "width": 500,
        "height": 500
      }
    ],
    "cartItem": [
      {
        "id": 1635848933221,
        "cartId": -1,
        "objId": "LcxYZnQeCoXqTnEmyeCq1w",
        "creationTime": 1635848933221,
        "count": 1,
        "shopId": 431782,
        "marketSku": "100131945690",
        "productId": 1720465387,
        "hid": 91491,
        "name": "Смартфон Xiaomi Redmi 4X 32GB, черный",
        "price": {
          "value": 9999,
          "currency": "RUR"
        },
        "fee": "THi2k-pxPNJcs24AmweTv7HnssfryvrwBYlxPyVQEzKv8zPAFzBzREdwjDQY_qz-gMdmi0bE7lJAgO3TjNsLs4Fw8m4ZX4HSMg37coULaxil90XnqzAUT56re7uEjVl6MgcQqng0NZ-nPnqNJt5s-mjPotphtU8osiaLMQr6evvvh9V2D4X12wBuouoxhNvF",
        "cartFee": "THi2k-pxPNJcs24AmweTv7HnssfryvrwBYlxPyVQEzKv8zPAFzBzREdwjDQY_qz-gMdmi0bE7lJAgO3TjNsLs4Fw8m4ZX4HSMg37coULaxil90XnqzAUT56re7uEjVl6MgcQqng0NZ-nPnqNJt5s-mjPotphtU8osiaLMQr6evvvh9V2D4X12wBuouoxhNvF",
        "feeShow": "THi2k-pxPNJcs24AmweTv7HnssfryvrwBYlxPyVQEzKv8zPAFzBzREdwjDQY_qz-gMdmi0bE7lJAgO3TjNsLs4Fw8m4ZX4HSMg37coULaxil90XnqzAUT56re7uEjVl6MgcQqng0NZ-nPnqNJt5s-mjPotphtU8osiaLMQr6evvvh9V2D4X12wBuouoxhNvF",
        "showPlaceId": "THi2k-pxPNJcs24AmweTv7HnssfryvrwBYlxPyVQEzKv8zPAFzBzREdwjDQY_qz-gMdmi0bE7lJAgO3TjNsLs4Fw8m4ZX4HSMg37coULaxil90XnqzAUT56re7uEjVl6MgcQqng0NZ-nPnqNJt5s-mjPotphtU8osiaLMQr6evvvh9V2D4X12wBuouoxhNvF",
        "slug": "smartfon-xiaomi-redmi-4x-32gb-chernyi",
        "isExpired": false,
        "promos": [],
        "isPrimaryInBundle": false,
        "label": "l4b9mdz3gzl",
        "pricedropPromoEnabled": false,
        "features": [],
        "isDirectShopInShop": false,
        "pp": 1809
      }
    ],
    "visibleEntity": [],
    "showPlace": [
      {
        "id": "THi2k-pxPNJcs24AmweTv2akn_hY-WuBUO5nXTQPOnwT8gFokXxATRdeqknkMUgi1Y7BBbDXNWfiKq714ZyHxqiPLOcKBWGxyZtIcXM8E32uFEKUvVkTbMiKLiuoXl5HvQFFzgjGS2C8f8G8dT6Wsk_eEjZolppz2oXB-pv578c,",
        "offerId": "LcxYZnQeCoXqTnEmyeCq1w",
        "feeShow": "THi2k-pxPNJcs24AmweTv2akn_hY-WuBUO5nXTQPOnwT8gFokXxATRdeqknkMUgi1Y7BBbDXNWfiKq714ZyHxqiPLOcKBWGxyZtIcXM8E32uFEKUvVkTbMiKLiuoXl5HvQFFzgjGS2C8f8G8dT6Wsk_eEjZolppz2oXB-pv578c,",
        "showUid": "16358937753910035464206000",
        "urls": {
          "cpa": "/safeclick/data=338FT8NBgRsBwTfDX0JTTL9-Vq8E-EqVjXqfY9n1OBv3uPh67uaAoT-iTEhVZbl7o5IACN0RtBvcd2H9_dkK5jYpUgyHsL0uPVwSERMa1ouPZuuMEHgagBDW0902I0Hhgau95NCy2bF5J1DW-t9EeL5RpE5EgLkAHnpl7OpCJ6pp_qQuOVK0kipAKWgr77OZajEGUTtSmWF2ve9-XUj7XklZ1U_bvrXsT33YPf6TkGZ-7kz6uV9zpwSmzNGRiR2GrQ8KEiGj7O6tluHoozowOsqIO1SyZlNwgjx7XsR7zYFO3j_VpZ0gnpdtFt8QPQ_On8ow96uNBFDh3IS71B9OIIZynE59j4mFRTVVcPmzPlR61GA7wJxFvT_nxD2l6S0RaFww1d2VXlOnJdtIbZep71cxnJHMoSXZzdihtILSZ4lkh7Vp1Fdibikvc4wMTTiXlWDRrjCSagDDPlbIbTPpP81ae9mc90H0XuDxQs4EHCOFAroh8Lv9Fm7AeGYHqbRa45327ePvgA78p0LSocT52U6XHD1rLTrK0dT1iehWDi9dohjpCXx2Uphojx4hyUPU_nuQ7bsQMFEWt7bMkjr0eXA5P2R8I6i0L94qMTxHfMATBnEfiLW9kUp5UhAbeUfiG5pzcik3reQ8XmBgpFZENsg7yL55rCgT2sM7l2dN3T-cW6e0jFIZQ67zI3BfsUKNJJnG8R2Ay1ArcyK5zeU2db5GBwFilMBfbYzWMz8vOKR0u0d9gpDk0Esia5RVNsp54jXo-NhSUfe1WpkiPAkKBV_Mac754Eh4bLAFdL2NXGnZecRgbDWKvv5R0vm8fHrHGOVt6qkrpDMwgBbYrhu0xcSVlqrimh1o2n7hY2P3WBHHx9uIFU9tNAevBDPa-HUEg0kglNbPqMO0jte8NY7Nld3y6q0VdupS8bFN2VMB2lP9guSBCnk8HpFwGhnR9-AnvA5_T9ioMIPVfbtDZUI5RN8uaNVYaxrN_1SXETYkeDzgoB0TX2UU8e5z6IjM1tOqhL5Denp3VmQ0VAdPzFOvoiO2Zw7b7WkuEfewdzm1KJ0__2kduTrSfihCh9NfwZAF0SHCK6cKNGiG4y3kFUJ1ovj_x7bKZo122GW479MIr35IjIR4PwTnprBVFY5O32BbRc8E4I9UKxGJpxxaMIe2mHApN3p8UyfYSICk_UfyeZGYGklzd_rpBOQj4UmZ1YksZIZUKbP8LlEuit8Qv7g1ZUlwDWri79YL/b64e=1/sign=b2506aa125c696404fe7d1209a3a0817/keyno=1/*",
          "direct": "https://pokupki.market.yandex.ru/product/100131945690?offerid=LcxYZnQeCoXqTnEmyeCq1w&cpc=ZS2RhJcSEPXNog7h0IISiutg70w0aqSg2E-ODX_phOh22Cluc911GMDbnX18BwBcNrFfVQAZ-TwOMwdZof1WzLGs8uEbCcrnGBFOC1dfZM2Zek4eYAuks6MNlHxwto2rVQzncZdM_Ip9fPGVHIA_hN9NtJZlfYozmLwU4gTYcqA,"
        },
        "cpc": "ZS2RhJcSEPXNog7h0IISiutg70w0aqSg2E-ODX_phOh22Cluc911GMDbnX18BwBcNrFfVQAZ-TwOMwdZof1WzLGs8uEbCcrnGBFOC1dfZM2Zek4eYAuks6MNlHxwto2rVQzncZdM_Ip9fPGVHIA_hN9NtJZlfYozmLwU4gTYcqA,",
        "promoIds": [],
        "entity": "showPlace",
        "offer": "LcxYZnQeCoXqTnEmyeCq1w"
      }
    ],
    "cartBusinessGroup": [
      {
        "id": "2_DEFAULT",
        "type": "DEFAULT",
        "cartItemIds": [
          1635848933221
        ],
        "title": "Доставка Яндекса и продавцов",
        "isDefaultGroup": true
      }
    ]
  }
}
```
