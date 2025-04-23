Модальное окно, которое рассказывает как использовать отчет

```jsx
const pages = [
    {
        title: 'Отчет по расходам на рекламу и ROI',
        text: 'Новый отчет поможет сравнивать расходы на разные рекламные каналы и их окупаемость — ROI (Retrurn on Investment). С детализацией вплоть до ключевой фразы.',
        imageSrc: 'https://avatars.mds.yandex.net/get-adv/28496/2a0000017134dab7768b185c036e4cb9bae7/orig',
        buttonText: 'Продолжить',
        linkText: 'Перейти в отчет',
        linkProps: {
            url: 'https://yandex.ru',
        },
    },
    {
        title: 'Расходы на любые рекламные каналы',
        text: 'Добавляйте в Метрику расходы на любые рекламные системы, трафик из которых вы разметили UTM-метками. Чем детальнее разметка, тем более подробными будут данные в отчете: по компании, креативу, ключевой фразе.',
        imageSrc: 'https://avatars.mds.yandex.net/get-adv/50995/2a0000017134e3270f5589e538499d25b9d1/orig',
        buttonText: 'Продолжить',
    },
    {
        title: 'Быстрая статистика по Директу',
        text: 'Расходы на Директ доступны в отчете сразу. Не нужно размечать ссылки из Директа UTM и загружать статистику в Метрику.',
        imageSrc: 'https://avatars.mds.yandex.net/get-adv/95093/2a0000017134de2b2c9f6253c5fc0e2c7728/orig',
        buttonText: 'Продолжить',
    },
    {
        title: 'ROI по любой цели с данными о доходе',
        text: 'Чтобы посмотреть ROI, выберите в отчете цель, для которой передается ценность, или соберите «Ecommerce-покупка».',
        imageSrc: 'https://avatars.mds.yandex.net/get-adv/50995/2a0000017134de70cc6792d8ad8325f8261c/orig',
        buttonText: 'Продолжить',
    },
    {
        title: 'Загрузка по API, через коннектор или вручную',
        text: 'Расходы можно добавить в Метрику по API, с помощью одно из коннекторов или вручную.<br/><br/><a href="#onboarding">Инструкция</a>',
        imageSrc: 'https://avatars.mds.yandex.net/get-adv/42259/2a0000017134dee01f55e6c5f5b474afaf14/orig',
        buttons: [
            {
                buttonText: 'Перейти в отчет',
            },
        ],
    },
];

<div style={{
    height: 640,
    position: 'relative',
    borderRadius: 16,
}}>
    <Onboarding pages={pages} />
</div>
```

```jsx
const pages = [
    {
        title: 'Оценивайте ROI каждого канала',
        text: 'ROI (Return on Investment) — это показатель окупаемости вложений. Чтобы в отчёте был показан ROI, нужны данные о доходе. Их можно передавать либо в ecommerce-данных, либо в качестве ценности цели. ROI (Return on Investment) — это показатель окупаемости вложений. Чтобы в отчёте был показан ROI, нужны данные о доходе. Их можно передавать либо в ecommerce-данных,  либо в качестве ценности цели.Чтобы в отчёте был показан ROI, нужны данные о доходе. Их можно передавать либо в ecommerce-данных,  либо в качестве ценности цели. ROI (Return on Investment) — это показатель окупаемости вложений. Чтобы в отчёте был показан ROI, нужны данные о доходе. Их можно передавать либо в ecommerce-данных, либо в качестве ценности цели. ROI (Return on Investment) — это показатель окупаемости вложений. Чтобы в отчёте был показан ROI, нужны данные о доходе. Их можно передавать либо в ecommerce-данных,  либо в качестве ценности цели.Чтобы в отчёте был показан ROI, нужны данные о доходе. Их можно передавать либо в ecommerce-данных,  либо в качестве ценности цели.',
        buttons: [
            {
                isInactive: true,
                buttonText: 'Перейти к отчету',
            },
            {
                buttonText: 'Загрузить расходы',
            },
        ],
    },
];

<div style={{
    height: 640,
    position: 'relative',
    borderRadius: 16,
}}>
    <Onboarding pages={pages} />
</div>
```

```jsx
const pages = [
    {
        title: 'Выберите способ загрузки расходов, чтобы начать работу',
        sections: [
            {
                text:
                    'Подготовьте простой <b>csv-файл</b> с <i>данными</i> по расходам.<br><a href="#onboarding">Подробнее</a>',
                buttonText: 'Загрузить файл',
                imageSrc: 'https://avatars.mds.yandex.net/get-adv/28496/2a0000017134dab7768b185c036e4cb9bae7/orig',
            },
            {
                text:
                    'Автоматизируйте загрузку данных о расходах с помощью API — потребуется помощь разработчика',
                buttonText: 'Загрузить по API',
                imageSrc: 'https://avatars.mds.yandex.net/get-adv/50995/2a0000017134e3270f5589e538499d25b9d1/orig',
            },
            {
                text:
                    'Подключите одну из интеграций, чтобы автоматически отправлять данные в Метрику',
                buttonText: 'Подключить интеграцию',
                imageSrc: 'https://avatars.mds.yandex.net/get-adv/95093/2a0000017134de2b2c9f6253c5fc0e2c7728/orig',
            },
        ],
    },
];

<div style={{
    height: 640,
    position: 'relative',
    borderRadius: 16,
}}>
    <Onboarding pages={pages} />
</div>
```
