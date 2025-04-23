# Резолвер resolveProductConfigurationByNavigationPath
Получение конфигурации виджета из CMS-документа.

## Параметры
| Parameter | Type     | Description  | Default Value |
|-----------|----------|--------------|---------------|
| `nid`     | number   | Id категории | 54415         |

## Пример запроса
```shell script
curl --request POST \
 --url '<FAPI host>/api/v1?name=resolveProductConfigurationByNavigationPath' \
 --header 'Content-Type: application/json' \
 --data '{"params": [{
  "nid": 34512430
 }]}'
```

## Пример ответа резолвера
```json
{
  result: [ 215834 ],
  collections: {
    productConfiguration: {
      '215834': {
        layout: [ 'layout' ],
        widgetsIds: [
          'redirectInfo',
          'gallery',
          'vendorLink',
          'summary',
          'filters',
          'offerInfo',
          'outOfStock',
          'warnings',
          'cashbackForNonPlus',
          'spreadDiscountReceipt',
          'installments',
          'credits',
          'set',
          'cheapestAsGift',
          'expressOfferInfo',
          'alternativeOffers',
          'priceFallSubscription',
          'link',
          'sponsoredOffer',
          'specs',
          'comparison',
          'instruction',
          'description',
          'descriptionReport',
          'banner',
          'links',
          'warnings',
          'reviewsSummary',
          'factors',
          'reviewsPhotoGallery',
          'leaveReview',
          'reviewSummaryDescription',
          'reviewsList',
          'questions',
          'richContent',
          'disclaimer',
          'faq',
          'resaleFeatures'
        ]
      }
    },
    productConfigurationWidgets: {
      redirectInfo: { id: 'redirectInfo', widgets: [], settings: { enabled: true } },
      gallery: { id: 'gallery', widgets: [], settings: { enabled: true } },
      vendorLink: { id: 'vendorLink', widgets: [], settings: { enabled: true } },
      summary: { id: 'summary', widgets: [], settings: { enabled: true } },
      filters: { id: 'filters', widgets: [], settings: { enabled: true } },
      offerInfo: { id: 'offerInfo', widgets: [], settings: { enabled: true } },
      outOfStock: { id: 'outOfStock', widgets: [], settings: { enabled: true } },
      warnings: { id: 'warnings', widgets: [], settings: { enabled: true } },
      cashbackForNonPlus: {
        id: 'cashbackForNonPlus',
        widgets: [],
        settings: { enabled: true }
      },
      spreadDiscountReceipt: {
        id: 'spreadDiscountReceipt',
        widgets: [],
        settings: { enabled: true }
      },
      installments: { id: 'installments', widgets: [], settings: { enabled: true } },
      credits: { id: 'credits', widgets: [], settings: { enabled: true } },
      set: { id: 'set', widgets: [], settings: { enabled: true } },
      cheapestAsGift: {
        id: 'cheapestAsGift',
        widgets: [],
        settings: { enabled: true }
      },
      expressOfferInfo: {
        id: 'expressOfferInfo',
        widgets: [],
        settings: { enabled: true }
      },
      alternativeOffers: {
        id: 'alternativeOffers',
        widgets: [],
        settings: { enabled: true }
      },
      priceFallSubscription: {
        id: 'priceFallSubscription',
        widgets: [],
        settings: { enabled: true }
      },
      link: { id: 'link', widgets: [], settings: { enabled: true } },
      sponsoredOffer: {
        id: 'sponsoredOffer',
        widgets: [],
        settings: { enabled: true }
      },
      specs: { id: 'specs', widgets: [], settings: { enabled: true } },
      comparison: { id: 'comparison', widgets: [], settings: { enabled: true } },
      instruction: { id: 'instruction', widgets: [], settings: { enabled: true } },
      description: { id: 'description', widgets: [], settings: { enabled: true } },
      descriptionReport: {
        id: 'descriptionReport',
        widgets: [],
        settings: { enabled: true }
      },
      banner: { id: 'banner', widgets: [], settings: { enabled: true } },
      links: { id: 'links', widgets: [], settings: { enabled: true } },
      reviewsSummary: {
        id: 'reviewsSummary',
        widgets: [],
        settings: { enabled: true }
      },
      factors: { id: 'factors', widgets: [], settings: { enabled: true } },
      reviewsPhotoGallery: {
        id: 'reviewsPhotoGallery',
        widgets: [],
        settings: { enabled: true }
      },
      leaveReview: { id: 'leaveReview', widgets: [], settings: { enabled: true } },
      reviewSummaryDescription: {
        id: 'reviewSummaryDescription',
        widgets: [],
        settings: { enabled: true }
      },
      reviewsList: { id: 'reviewsList', widgets: [], settings: { enabled: true } },
      questions: { id: 'questions', widgets: [], settings: { enabled: true } },
      richContent: { id: 'richContent', widgets: [], settings: { enabled: true } },
      disclaimer: { id: 'disclaimer', widgets: [], settings: { enabled: true } },
      faq: {
        id: 'faq',
        widgets: [],
        settings: {
          enabled: true,
          title: 'Заголовок FAQ для "Все товары" - NID - 54415',
          questionsWithAnswers: [
            {
              question: 'Вопрос ресейла для "Все товары" - №1',
              answer: 'NID - 54415'
            },
            {
              question: 'Вопрос ресейла для "Все товары" - №2',
              answer: 'NID - 54415'
            }
          ]
        }
      },
      resaleFeatures: {
        id: 'resaleFeatures',
        widgets: [],
        settings: {
          enabled: true,
          resaleReasonTexts: [
            { key: '3', text: 'витринный образец' },
            { key: '4', text: 'уценка' }
          ],
          resaleConditionTexts: [
            { key: 'resale_perfect', text: 'Идеальное' },
            { key: 'resale_excellent', text: 'Отличное' },
            { key: 'resale_well', text: 'Хорошее' }
          ]
        }
      }
    },
    productConfigurationLayout: {
      layout: { id: 'layout', name: 'KM_MOBILE_DEFAULT', type: 'MobileLayout' }
    }
  }
}
```

## Ссылки:
- [Входные параметры](https://a.yandex-team.ru/arcadia/market/front/apps/marketfront/src/resolvers/cms/productConfigation/resolveProductConfigurationByNavigationPath.js:17)
