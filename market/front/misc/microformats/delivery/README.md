# Микроформат блока delivery
Блок содержит в себе информацию о доставке

## Инсайд от репорта
На самом деле там под капотом енум с иерархией крутости доставки
```
enum DeliveryType {
            /// shop is not able to deliver to user
            None = 0,

            /// shop can deliver to user from other region
            Exists = 1,

            /// shop has delivery in the same country user is in
            Country = 2,

            /// shop has outlets in user region or downloadable
            Priority = 3
        };
```
