### Обновление порогов для таймингов ручек бэкендов Фронтенда Маркета        

| Имя бэкенда | Имя приложения | Ручка | Прежнее значение TTLB | Новое значение TTLB | Разница TTLB % | Прежнее значение RPS | Новое значение RPS | Разница RPS % | Комментарий |
| ----------- | -------------- | ----- | --------------------- | ------------------- | -------------- | -------------------- | ------------------ | ------------- | ----------- |
| market_report | white_desktop | getModelsById | 350 | 399 | 14% | 900 | 918 | 2% | 📊 Изменение показателей |
| market_report | white_desktop | getProductsInfo | 350 | 413 | 18% | 800 | 762 | -5% | 📊 Изменение показателей |
| market_report | white_desktop | search_byText | 1500 | 1931 | 29% | 150 | 138 | -8% | 📊 Изменение показателей |
| market_report | white_desktop | getProductShopsOnline | 250 | 289 | 16% | 600 | 683 | 14% | 📊 Изменение показателей |
| market_report | white_desktop | getRecipeFromFilters | 500 | 906 | 81% | 200 | 153 | -23% | 📊 Изменение показателей |
| market_report | white_desktop | search_byCategory | 1900 | 2483 | 31% | 70 | 95 | 36% | 📊 Изменение показателей |
| market_report | white_desktop | getProductRecipes | 340 | 379 | 11% | 232 | 191 | -18% | 📊 Изменение показателей |
| market_report | white_desktop | getAlsoViewed | 700 | 1075 | 54% | 91 | 204 | 124% | 📊 Изменение показателей |
| market_report | white_desktop | getTopOffersForProduct | 500 | 596 | 19% | 763 | 508 | -33% | 📊 Изменение показателей |
| market_report | white_desktop | getProductOffers | 1200 | 486 | -59% | 40 | 296 | 640% | 📊 Изменение показателей |
| market_report | white_desktop | getOffersByProductIdAndShopId | 300 | 407 | 36% | 293 | 316 | 8% | 📊 Изменение показателей |
| market_report | white_desktop | getVendorUpsale | 305 | 359 | 18% | 100 | 145 | 45% | 📊 Изменение показателей |
| market_report | white_desktop | fetchDeliveryConditions | 0 | 545 | — | 0 | 66 | — | 📈 Новая ручка |
| market_report | white_desktop | getRecipesListFromFilters | 250 | 265 | 6% | 100 | 72 | -28% | 📊 Изменение показателей |
| market_report | white_desktop | getVendorIncut | 400 | 359 | -10% | 80 | 71 | -11% | 📊 Изменение показателей |
| market_report | white_desktop | getProductsByHistoryEx | 700 | 1375 | 96% | 41 | 49 | 20% | 📊 Изменение показателей |
| market_report | white_desktop | search_byTextInCategory | 1600 | 2053 | 28% | 40 | 44 | 10% | 📊 Изменение показателей |
| market_report | white_desktop | getAttractiveModels | 700 | 905 | 29% | 110 | 76 | -31% | 📊 Изменение показателей |
| market_report | white_desktop | getShopsInfo | 250 | 285 | 14% | 200 | 131 | -34% | 📊 Изменение показателей |
| market_report | white_desktop | getSearchResultsByOfferIds | 0 | 353 | — | 0 | 68 | — | 📈 Новая ручка |
| market_report | white_desktop | getGroupFilters | 250 | 257 | 3% | 170 | 158 | -7% | 📊 Изменение показателей |
| market_report | white_desktop | getPersonalRecommendations | 600 | 0 | -100% | 7 | 0 | -100% | ♻️ Больше не следим |
| market_report | white_desktop | getBusinessInfo | 250 | 187 | -25% | 60 | 20 | -67% | 📊 Изменение показателей |
| market_report | white_desktop | getPrime | 1100 | 1802 | 64% | 47 | 23 | -51% | 📊 Изменение показателей |
| market_report | white_desktop | search_byShop | 865 | 0 | -100% | 1 | 0 | -100% | ♻️ Больше не следим |
| market_report | white_desktop | fetchPrime | 1200 | 731 | -39% | 40 | 106 | 165% | 📊 Изменение показателей |
| market_report | white_touch | getModelsById | 186 | 299 | 61% | 750 | 427 | -43% | 📊 Изменение показателей |
| market_report | white_touch | search_byText | 1300 | 1442 | 11% | 210 | 177 | -16% | 📊 Изменение показателей |
| market_report | white_touch | getSearchResultsByOfferIds | 320 | 416 | 30% | 232 | 196 | -16% | 📊 Изменение показателей |
| market_report | white_touch | getOffersByProductIdAndShopId | 250 | 328 | 31% | 122 | 209 | 71% | 📊 Изменение показателей |
| market_report | white_touch | getProductOffers | 370 | 527 | 42% | 342 | 270 | -21% | 📊 Изменение показателей |
| market_report | white_touch | search_byCategory | 1400 | 1686 | 20% | 95 | 106 | 12% | 📊 Изменение показателей |
| market_report | white_touch | fetchDeliveryConditions | 0 | 242 | — | 0 | 50 | — | 📈 Новая ручка |
| market_report | white_touch | getProductRecipes | 650 | 262 | -60% | 110 | 106 | -4% | 📊 Изменение показателей |
| market_report | white_touch | getProductBundle | 150 | 238 | 59% | 100 | 106 | 6% | 📊 Изменение показателей |
| market_report | white_touch | getVendorUpsale | 350 | 271 | -23% | 85 | 102 | 20% | 📊 Изменение показателей |
| market_report | white_touch | getAlsoViewedProducts | 550 | 541 | -2% | 107 | 91 | -15% | 📊 Изменение показателей |
| market_report | white_touch | search_byTextInCategory | 1300 | 1493 | 15% | 60 | 48 | -20% | 📊 Изменение показателей |
| market_report | white_touch | getRecipeFromFilters | 125 | 222 | 78% | 57 | 35 | -39% | 📊 Изменение показателей |
| market_report | white_touch | getRecipesListFromFilters | 140 | 211 | 51% | 57 | 35 | -39% | 📊 Изменение показателей |
| market_report | white_touch | getVendorIncut | 450 | 440 | -2% | 40 | 34 | -15% | 📊 Изменение показателей |
| market_report | white_touch | getSkuById | 300 | 281 | -6% | 40 | 39 | -2% | 📊 Изменение показателей |
| market_report | white_touch | getProductAnalogues | 750 | 706 | -6% | 24 | 21 | -12% | 📊 Изменение показателей |
| market_report | white_touch | getShopsInfo | 150 | 240 | 60% | 32 | 29 | -9% | 📊 Изменение показателей |
| market_report | white_touch | fetchPrime | 1100 | 714 | -35% | 82 | 70 | -15% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchSkusWithProducts | 430 | 358 | -17% | 196 | 266 | 36% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchAvailableDelivery | 175 | 232 | 33% | 225 | 277 | 23% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchRecipesByProductId | 120 | 204 | 70% | 145 | 194 | 34% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchAlsoViewed | 325 | 823 | 153% | 39 | 70 | 79% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchComplementaryProductGroups | 500 | 418 | -16% | 75 | 67 | -11% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchDeliveryConditions | 0 | 595 | — | 0 | 28 | — | 📈 Новая ручка |
| market_report | blue_desktop | fetchPrime | 1700 | 4630 | 172% | 94 | 80 | -15% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchRecipeByFilter | 303 | 414 | 37% | 49 | 30 | -39% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchAccessories | 0 | 458 | — | 0 | 18 | — | 📈 Новая ручка |
| market_report | blue_desktop | fetchAttractiveModels | 510 | 689 | 35% | 18 | 18 | 0% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchProductsByHistory | 300 | 443 | 48% | 17 | 17 | 0% | 📊 Изменение показателей |
| market_report | blue_desktop | fetchCombinedStrategies | 0 | 1110 | — | 0 | 12 | — | 📈 Новая ручка |
| market_report | blue_touch | fetchAvailableDelivery | 200 | 284 | 42% | 80 | 113 | 41% | 📊 Изменение показателей |
| market_report | blue_touch | fetchSkusWithProducts | 260 | 388 | 49% | 73 | 105 | 44% | 📊 Изменение показателей |
| market_report | blue_touch | fetchRecipesByProductId | 180 | 254 | 41% | 47 | 75 | 60% | 📊 Изменение показателей |
| market_report | blue_touch | fetchAlsoViewed | 361 | 1229 | 240% | 24 | 67 | 179% | 📊 Изменение показателей |
| market_report | blue_touch | fetchComplementaryProductGroups | 500 | 446 | -11% | 65 | 66 | 2% | 📊 Изменение показателей |
| market_report | blue_touch | fetchPrime | 1900 | 4519 | 138% | 60 | 54 | -10% | 📊 Изменение показателей |
| market_report | blue_touch | fetchDeliveryConditions | 0 | 422 | — | 0 | 25 | — | 📈 Новая ручка |
| market_report | blue_touch | fetchRecipeByFilter | 0 | 366 | — | 0 | 14 | — | 📈 Новая ручка |
