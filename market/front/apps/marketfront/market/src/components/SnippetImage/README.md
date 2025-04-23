### Примеры


#### Дефолтный вид

```jsx
    <SnippetImage
        url="https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq"
    />
```

#### Без заданного `url`

```jsx
    <SnippetImage
    />
```

#### `fullWidth`

Растягивает картинку на всю ширину контейнера.

```jsx
    <div style={{width: '150px'}}>
        <SnippetImage
            fullWidth
            url="https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq"
        />
    </div>
```

#### `fullHeight`

Растягивает картинку до высоты контейнера.

```jsx
    <div style={{height: '150px'}}>
        <SnippetImage
            fullHeight
            url="https://avatars.mds.yandex.net/get-mpic/96484/img_id1104062486833029182/6hq"
        />
    </div>
```
