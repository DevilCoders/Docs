## Манифест 

JSON-файл с описанием как открывать вебвью и как обновлять статику.

Настраивается в [конфиге вебпака](../../client/webpack/webpack.mobile.extras.js)

### Описание структуры

```json lines
{
    // Хост на котором будет открываться точка входа в вебвью
    "dynamic_host": "https://mail.{{DOMAIN}}",
    
    // Используется для вычисления имени файла с статикой
    "static_url": "https://yastatic.net/s3/psf/contact-card/",
    
    "yandex": {
    // Строка названием версии.
    // Версии сравниваются как строки
    // При любом несовпадении мобильное приложение должно начать обновлять статику.
    "app_version": "0.9.1",
    
    "prefetch": [
    {
        "name": "manifest",
        
        // Урл по которому мобильное приложение будет искать новый манифест
        "url": "https://calendar.{{DOMAIN}}/manifest/contact-card",
        
        // Период проверки ручки с манифестом
        "period_minutes": 120
    }
    ],
    "cache": {
        // Список файлов с статикой для кеширования мобильным приложением
        // Важно иметь хеши, приложение обновляет только дифф между предыдущим манифестом
        "resources": [
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.contact-card.en-b06cd45d038e30ee019c.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.contact-card.ru-6baa7021ea24bdc96f99.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.contact-card.tr-17d2badc7abd6c5ae2b2.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.contact-card.uk-5de7b9addd480f44896d.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.gap.en-5bd799df04cd772aec4f.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.gap.ru-c9e0969396faec02384d.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.gap.tr-6ad12a6ed9bfe115c7c9.js",
            "https://yastatic.net/s3/psf/contact-card/i18n.mail-liza.gap.uk-054e1461f2309bd7f9bb.js",
            "https://yastatic.net/s3/psf/contact-card/index-c032655f57ff02794b74.css",
            "https://yastatic.net/s3/psf/contact-card/index-c032655f57ff02794b74.js",
            "https://yastatic.net/s3/psf/contact-card/ba48b9267607ec0f9731b6f95cdc788f-index.html",
            "https://yastatic.net/s3/psf/contact-card/index-c032655f57ff02794b74.js.LICENSE.txt",
            "https://yastatic.net/s3/psf/contact-card/noAvatar-dc81da2cca9b5b00ab218648ec83028f.png",
            "https://yastatic.net/islands/_/KRBKbh7904nwfw8-FzDelXRpZ9o.woff2",
            "https://yastatic.net/islands/_/_Ocpq376VVJdR5aDIq4WkfWF6Gg.woff2",
            "https://yastatic.net/islands/_/TR2STky64Ra69XlYzqKN7cnjYfQ.woff2",
            "https://yastatic.net/islands/_/kxV2-EeUdyizF_lxQ-hrmltgp3c.woff2"
        ]
    }
},

// Урл с точкой входа для вебвью. Обычно html файл
"index_page": "https://yastatic.net/s3/psf/contact-card/ba48b9267607ec0f9731b6f95cdc788f-index.html"
}
```
