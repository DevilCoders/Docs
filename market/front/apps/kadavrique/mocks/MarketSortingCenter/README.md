# Market Sorting Center (TPL Sorting Center)

## Swagger оригинального бекенда

https://sc-int.tst.vs.market.yandex.net/swagger-ui.html

## Описание state

```jsMin
{
  "marketLogistics": {
    "collections": {
      "cells": {
        "123": {
          // cellDto
        }
      },
      "cellsForLots": {
        "123": {
          // cellForLotDto
        }
      },
      "cellSubTypes": {
        [cell-type]: CellSubType[]
      },
      "cellTypes": {
        [collection-name]: CellType[]
      },
      "allCouriers": {id: number; name: string}[],
      "couriers": {
        "123": {
          // courierDto
        }
      },
      "courierFilters": {
        "123": {
          // courierFilterDto
        }
      },
      midMilesCouriers: {
        "12": {
          // midMilesCourierDto
        }
      },
      "dispatchPersonFilters": {
        "123": {
          // dispatchPersonFilterDto
        }
      },
      "filters": {
        "filter-name": FilterDto[],
      }
      "events": {
        "123": OrderEventDto[], // orderId
      }
      "orders": {
        "12": {
          // orderDto
        }
      },
      "routes": {
        "12": {
          // routeDto
        }
      },
      "routeCategories": {
        "routeType": []
      },
      "scFeatures": {
        "featureName" boolean
      },
      "inboundRegistries": {
        "warehouseId": inboundRegistryDto[]
      },
      "users": {
        "123": {
          // userDto
        }
      },
      "userRoles": UserRole[],
      "zones": {
        "123": {
          // zoneDto
        }
      },
      "warehouses": {
        "123": {
          // warehouseDto
        }
      },
      "lots": {
         "123": {
            // lotDto
          }
       }
    },
  }
}
```

## Замоканные пути

##### partner-cell-controller
- **GET** /internal/partners/\<scPartnerId>/cells/buffer
- **GET** /internal/partners/\<scPartnerId>/cells/forLots
- **GET** /internal/partners/\<scPartnerId>/cells/<cellId>
- **PUT** /internal/partners/\<scPartnerId>/cells/<cellId>
- **DELETE** /internal/partners/\<scPartnerId>/cells/<cellId>
- **GET** /internal/partners/\<scPartnerId>/cells
- **POST** /internal/partners/\<scPartnerId>/cells
- **GET** /internal/partners/\<scPartnerId>/cellSubtypes
- **GET** /internal/partners/\<scPartnerId>/cellTypes

##### partner-courier-controller
- **GET** /internal/partners/\<scPartnerId>/couriers
- **GET** /internal/partners/\<scPartnerId>/couriers/midMiles

##### partner-features-controller
- **GET** /internal/partners/\<scPartnerId>/features

##### partner-order-controller
- **GET** /internal/partners/\<scPartnerId>/orders
- **POST** /internal/partners/\<scPartnerId>/orders/<orderId>/markAsDamaged

##### partner-inbound-controller
- **PUT** /internal/partners/<scPartnerId>/inbounds/<inboundId>/performAction/<action>
- **GET** /internal/partners/<scPartnerId>/inbounds
- **GET** /internal/partners/<scPartnerId>/inbounds/types
- **GET** /internal/partners/<scPartnerId>/inbounds/statuses

##### partner-order-filter-controller
- **GET** /internal/partners/\<scPartnerId>/orders/filters/dispatchPerson

##### partner-order-history-controller
- **GET** /internal/partners/\<scPartnerId>/orders/<orderId>/events

##### partner-route-controller
- **PUT** /internal/partners/\<scPartnerId>/routes/<routeId>/courier
- **GET** /internal/partners/\<scPartnerId>/routes/fullInfo
- **GET** /internal/partners/\<scPartnerId>/routes/mainInfo
- **GET** /internal/partners/\<scPartnerId>/routes/page
- **GET** /internal/partners/\<scPartnerId>/routes/summary
- **GET** /internal/partners/\<scPartnerId>/routes/categories

##### partner-users-controller
- **GET** /internal/partners/\<scPartnerId>/users/roles
- **GET** /internal/partners/\<scPartnerId>/users/<userId>
- **PUT** /internal/partners/\<scPartnerId>/users/<userId>
- **DELETE** /internal/partners/\<scPartnerId>/users/<userId>
- **GET** /internal/partners/\<scPartnerId>/users
- **POST** /internal/partners/\<scPartnerId>/users

##### partner-warehouse-controller
- **GET** /internal/partners/\<scPartnerId>/warehouses

##### partner-zone-controller
- **GET** /internal/partners/\<scPartnerId>/zones/<zoneId>
- **PUT** /internal/partners/\<scPartnerId>/zones/<zoneId>
- **DELETE** /internal/partners/\<scPartnerId>/zones/<zoneId>
- **GET** /internal/partners/\<scPartnerId>/zones
- **POST** /internal/partners/\<scPartnerId>/zones

##### lots-controller
- **PUT** /internal/partners/\<scPartnerId>/lots/<routeId>
- **GET** /internal/partners/\<scPartnerId>/lots
- **POST** /internal/partners/\<scPartnerId>/lots
- **DELETE** /internal/partners/\<scPartnerId>/lots/<lotId>
