## Основные параметры

    {
        "block": "share",
        "socials": "facebook,odnoklassniki,telegram,google,twitter,vkontakte,whatsapp,viber"
    }

## Передача кастомных переводов

    {
        "block": "share",
        "socials": "facebook,odnoklassniki,telegram,google,twitter,vkontakte,whatsapp,viber",
        "texts": {
            "more": "Ещё",
            "vkontakte": "ВКонтакте"
        }
    }

## При нажатии на «Ещё» открывать попап со списком соцсетей, а не добавлять ещё кнопок:

    {
        "block": "share",
        "socials": "facebook,odnoklassniki,telegram,google,twitter,vkontakte,whatsapp,viber",
        "hasPopup": true
    }

## Уменьшить количество кнопок в первом ряду

    {
        "block": "share",
        "socials": "facebook,odnoklassniki,telegram,google,twitter,vkontakte,whatsapp,viber",
        "firstRowButtons": 2
    }

## Оставить только одну кнопку «Поделиться» с иконкой, как на Погоде:

    {
        "block": "share",
        "socials": "facebook,odnoklassniki,telegram,google,twitter,vkontakte,whatsapp,viber",
        "firstRowButtons": 0,
        "hasPopup": true,
        "hasMoreIcon": true,
        "texts": {
            "more": "Поделиться"
        }
    }
