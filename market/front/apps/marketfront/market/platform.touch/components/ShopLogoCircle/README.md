Отображает круглое лого магазина или заглушку
### Параметры

#### size === 'big'

```jsx
<ShopLogoCircle size="big" />
```

#### size === 'small'

```jsx
<ShopLogoCircle size="small" />
```


#### shop

сущность магазина со слагом и логотипом

```json
{
    "id": 1, 
    "name": "test", 
    "shopName": "test", 
    "slug": "shop", 
    "logo": "url"
}
```

```jsx
<ShopLogoCircle 
    shop={{id: 1, name: 'test', shopName: 'test', slug: 'shop', logo: '//avatars.mds.yandex.net/get-market-shop-logo/1598257/2a00000167d200f1bcfac507cd233f3ca50f/orig'}} 
/>
```

#### link

ссылка на магазин

```jsx
<ShopLogoCircle 
    shop={{id: 1, name: 'test', shopName: 'test', slug: 'shop', logo: '//avatars.mds.yandex.net/get-market-shop-logo/1598257/2a00000167d200f1bcfac507cd233f3ca50f/orig'}}
    link="https://market.yandex.ru" 
/>
```


#### className

кастомный класс
