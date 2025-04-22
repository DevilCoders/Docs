### Элемент заказа


```jsx

const thumbnails = [{"containerWidth": 50, "containerHeight": 50, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/50x50", "width": 35, "height": 50 }, {"containerWidth": 55, "containerHeight": 70, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/55x70", "width": 49, "height": 70 }, {"containerWidth": 60, "containerHeight": 80, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/60x80", "width": 56, "height": 80 }, {"containerWidth": 74, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/74x100", "width": 70, "height": 100 }, {"containerWidth": 75, "containerHeight": 75, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/75x75", "width": 53, "height": 75 }];


<Helper.Playground
    component={OrderItem}
    defaultValues={{
        title: 'Мультимедиа-платформа Яндекс.Станция, фиолетовая',
        count: 1,
    }}
    example={props => {
        return (
            <div>
                <OrderItem
                    {...props}
                    thumbnails={thumbnails}
                />
            </div>
        );
    }}
/>
```
