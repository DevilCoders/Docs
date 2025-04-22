### Изображение

Отрисовывает картинку

```jsx
import Text from '@self/root/src/uikit/components/Text';
const DropdownNative = require('@self/root/src/uikit/components/DropdownNative').default;
const styles = require('./Readme.styles.styl');

const Container = ({width, height, title, children}) => (
    <div className={styles.root} style={{
        width: width ? (width+2) : undefined,
    }}>
        <Text>{title}</Text>
        <div className={styles.block} style={{
            height,
            width,
        }}>
            {children}
        </div>
    </div>
);


state = {
    value: '1',
    images: [
        {
            value: '1',
            text: 'Колонка',
            src: '//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/5hq',
            srcSet: '//avatars.mds.yandex.net/get-mpic/1382936/img_id3557252912121609779.png/9hq 2.5x',
        },
        {
            value: '2',
            text: 'Термокружка',
            src: '//avatars.mds.yandex.net/get-mpic/1215212/img_id1480594839207247629.jpeg/x166_trim',
            srcSet: '//avatars.mds.yandex.net/get-mpic/1215212/img_id1480594839207247629.jpeg/x248_trim 2.5x',
        },
        {
            value: '3',
            text: 'Видеокарта',
            src: '//avatars.mds.yandex.net/get-mpic/175985/img_id8219806329444655489/x166_trim',
            srcSet: '//avatars.mds.yandex.net/get-mpic/175985/img_id8219806329444655489/x248_trim 2.5x',
        },
    ],
};


const getImage = () => state.images.find((image) => image.value === state.value);
const getValue = () => getImage().value;
const getSrc = () => getImage().src;
const getSrcSet = () => getImage().srcSet;

const onChangeSelector = ({currentTarget: {value}}) => setState({value});

<div>
    <h3>Выберите изображение:</h3>
    <DropdownNative options={state.images} onChange={onChangeSelector} value={getValue()}/>

    <h3>Подстраивается под размер контейнера</h3>
    <hr />
    <div style={{display: 'flex', flexWrap: 'wrap', alignItems: 'flex-end'}}>
        <Container width={800} height={250} title=''>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
                fillParent
            />
        </Container>

        <Container width={250} height={250} title='Изображение ограничено размером 150px'>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
                maxSize={150}
                fillParent
            />
        </Container>

        <Container width={150} height={250} title=''>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
                fillParent
            />
        </Container>

        <Container width={250} height={150} title=''>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
                fillParent
            />
        </Container>
    </div>

    <h3>Не подстраивается под размер контейнера</h3>
    <hr />
    <div style={{display: 'flex', flexWrap: 'wrap', alignItems: 'flex-end'}}>
        <Container width={800} height={250} title=''>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
            />
        </Container>

        <Container width={250} height={250} title='Изображение ограничено размером 150px'>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
                maxSize={150}
            />
        </Container>

        <Container width={150} height={250} title=''>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
            />
        </Container>

        <Container width={250} height={150} title=''>
            <Image
                src={getSrc()}
                srcSet={getSrcSet()}
            />
        </Container>
    </div>

    <Text size={'100'}>PS: Во всех случаях берём изображение 200x200, размер контейнера 300px</Text>

</div>
```
