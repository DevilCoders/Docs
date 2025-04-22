### Изображение

Находит ближайшую по размерам миниатюру и отображает её в соответствии с переданными размерами.

```jsx
import Text from '@self/root/src/uikit/components/Text';

const Container = ({width, height, title, children}) => (
    <div style={{
        width: width ? (width+2) : undefined,
        overflow: 'hidden'
    }}>
        <Text>{title}</Text>
        <div style={{height, width, border: '1px dashed blue'}}>
            {children}
        </div>
    </div>
);

const thumbnails = [{"containerWidth": 50, "containerHeight": 50, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/50x50", "width": 35, "height": 50 }, {"containerWidth": 55, "containerHeight": 70, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/55x70", "width": 49, "height": 70 }, {"containerWidth": 60, "containerHeight": 80, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/60x80", "width": 56, "height": 80 }, {"containerWidth": 74, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/74x100", "width": 70, "height": 100 }, {"containerWidth": 75, "containerHeight": 75, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/75x75", "width": 53, "height": 75 }, {"containerWidth": 90, "containerHeight": 120, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/90x120", "width": 85, "height": 120 }, {"containerWidth": 100, "containerHeight": 100, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/100x100", "width": 70, "height": 100 }, {"containerWidth": 120, "containerHeight": 160, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/120x160", "width": 113, "height": 160 }, {"containerWidth": 150, "containerHeight": 150, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/150x150", "width": 106, "height": 150 }, {"containerWidth": 180, "containerHeight": 240, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/180x240", "width": 170, "height": 240 }, {"containerWidth": 190, "containerHeight": 250, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/190x250", "width": 177, "height": 250 }, {"containerWidth": 200, "containerHeight": 200, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/200x200", "width": 141, "height": 200 }, {"containerWidth": 240, "containerHeight": 320, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/240x320", "width": 226, "height": 320 }, {"containerWidth": 300, "containerHeight": 300, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/300x300", "width": 212, "height": 300 }, {"containerWidth": 300, "containerHeight": 400, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/300x400", "width": 283, "height": 400 }, {"containerWidth": 600, "containerHeight": 600, "url": "//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/600x600", "width": 425, "height": 600 } ];
const stabComponent = <Text>не найдено</Text>;

<div>
    <h3>Подстраивается под размер контейнера</h3>
    <hr />
    <div style={{display: 'flex', flexWrap: 'wrap', alignItems: 'flex-end'}}>
        <Container width={800} height={250} title=''>
            <Picture
                size={200}
                thumbnails={thumbnails}
                stabComponent={stabComponent}
                fillParent
            />
        </Container>

        <Container width={250} height={250} title='Изображение ограничено размером 150px'>
            <Picture
                thumbnails={thumbnails}
                size={250}
                maxSize={150}
                stabComponent={stabComponent}
                fillParent
            />
        </Container>

        <Container width={150} height={250} title=''>
            <Picture
                thumbnails={thumbnails}
                stabComponent={stabComponent}
                size={200}
                fillParent
            />
        </Container>

        <Container width={250} height={150} title=''>
            <Picture
                thumbnails={thumbnails}
                stabComponent={stabComponent}
                size={200}
                fillParent
            />
        </Container>
    </div>

    <h3>Не подстраивается под размер контейнера</h3>
    <hr />
    <div style={{display: 'flex', flexWrap: 'wrap', alignItems: 'flex-end'}}>
        <Container width={800} height={250} title=''>
            <Picture
                size={200}
                thumbnails={thumbnails}
                stabComponent={stabComponent}
            />
        </Container>

        <Container width={250} height={250} title='Изображение ограничено размером 150px'>
            <Picture
                thumbnails={thumbnails}
                size={250}
                maxSize={150}
                stabComponent={stabComponent}
            />
        </Container>

        <Container width={150} height={250} title=''>
            <Picture
                thumbnails={thumbnails}
                stabComponent={stabComponent}
                size={200}
            />
        </Container>

        <Container width={250} height={150} title=''>
            <Picture
                thumbnails={thumbnails}
                stabComponent={stabComponent}
                size={200}
            />
        </Container>
    </div>

</div>
```
