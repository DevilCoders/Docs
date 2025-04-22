Пропорционально масштабируюясь, занимает всю высоту контейнера.
Если высота не задана, то пропорционально масштабируюясь, занимает всю ширину контейнера.

## Песочница
```jsx noeditor

    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <Helper.Playground
            component={BannerLight}
            settings={{background: 'transparent'}}
            defaultValues={{
                link: '/index2',
                height: 100,
            }}
            example={({link, align, height, image = {
                entity: 'picture',
                thumbnail: {
                    entity: 'thumbnail',
                    width: '373',
                    height: '158',
                    densities: [
                        {
                            entity: 'density',
                            id: 1,
                            url: '//avatars.mds.yandex.net/get-mpic/1215212/cms_resources-navigation-pages-48495-15cbd410de4165fdf57499240350f5f1.png/optimize'
                        },
                        {
                            entity: 'density',
                            id: 2,
                            url: '//avatars.mds.yandex.net/get-mpic/1331400/cms_resources-navigation-pages-48495-6ce81742bc7bfc7696de07b98590e037_1020x272@x2.jpeg/optimize'
                        }
                    ]
                }
            }}) => (
                <div style={{
                    width: 500,
                    height: 120,
                    resize: 'both',
                    overflow: 'hidden',
                    padding: '10px',
                    background: 'black',
                }}>
                    <BannerLight {...{image, link, align, height}} />
                </div>
            )}
        />
    </Provider>
```

## Banner с высотой
```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <BannerLight
        {...{
          height: 300,
          link: '/index2',
          image: {
              entity: 'picture',
              thumbnail: {
                  entity: 'thumbnail',
                  width: '373',
                  height: '158',
                  densities: [
                      {
                          entity: 'density',
                          id: 1,
                          url: '//avatars.mds.yandex.net/get-mpic/1215212/cms_resources-navigation-pages-48495-15cbd410de4165fdf57499240350f5f1.png/optimize'
                      },
                      {
                          entity: 'density',
                          id: 2,
                          url: '//avatars.mds.yandex.net/get-mpic/1331400/cms_resources-navigation-pages-48495-6ce81742bc7bfc7696de07b98590e037_1020x272@x2.jpeg/optimize'
                      }
                  ]
              }
          },
          align: 'center',
        }}
        />
    </Provider>
```

## Banner без высоты
```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const store = createStore(() => ({
        collections: {},
    }));

    <Provider store={store}>
        <BannerLight
        {...{
          link: '/index2',
          image: {
              entity: 'picture',
              thumbnail: {
                  entity: 'thumbnail',
                  width: '373',
                  height: '158',
                  densities: [
                      {
                          entity: 'density',
                          id: 1,
                          url: '//avatars.mds.yandex.net/get-mpic/1215212/cms_resources-navigation-pages-48495-15cbd410de4165fdf57499240350f5f1.png/optimize'
                      },
                      {
                          entity: 'density',
                          id: 2,
                          url: '//avatars.mds.yandex.net/get-mpic/1331400/cms_resources-navigation-pages-48495-6ce81742bc7bfc7696de07b98590e037_1020x272@x2.jpeg/optimize'
                      }
                  ]
              }
          },
          align: 'center',
        }}
        />
    </Provider>
```
