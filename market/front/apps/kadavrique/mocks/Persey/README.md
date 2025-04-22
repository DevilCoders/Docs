# Persey

Данные в стейте:

```
{
    "Persey.collections": {
        subscriptions: {
            brands: {
                ...
                [key: BrandName]: { // ключ бренда, например "market"
                    subs_info?: {
                        mod: {
                            value: number, // значение округления
                            repr: {
                                /**
                                 * Строка с форматом отображения значения округления вида "100 $SIGN$$CURRENCY$"
                                 * В маркете пока не используется
                                 */
                                amount: string,
                                /**
                                 * Код валюты (пока считаем, что будет только RUB), на маркете мапится в валюту (RUB -> RUR)
                                 */
                                currency_code: 'RUB',
                            },
                        },
                        /**
                         * Информация с целью пожертвования. Тут будут перечислены фонды, в которые пользователь жертвует деньги
                         */
                        goal: {
                            fund_id: string,
                            city?: string,
                            category?: string,
                            partner?: string,
                        },
                    },
                    contribution?: { // размер пожертвования
                        /**
                         * Строка с форматом отображения размера пожертвования вида "100 $SIGN$$CURRENCY$"
                         * В маркете пока не используется
                         */
                        amount: string,
                        currency_code: 'RUB',
                    }
                }
                ...
            }
        }
    },
}
```
