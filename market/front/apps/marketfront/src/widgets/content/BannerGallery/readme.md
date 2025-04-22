### Виджет 'Галерея баннеров'
Возможность размещать несколько баннеров в одну строку

```jsx
    const Provider = require('react-redux').Provider;
    const createStore = require('redux').createStore;
    const ViewPort = require('@self/root/src/components/Styleguidist/ViewPort').default;
    const View = require('./BannerGallery').default;
    const withWidgetWrapper = require('@self/root/src/components/HOC/withWidgetWrapper').default;

    const props = {
        banners: [
          {id: 'id1', schema: 'banner'},
          {id: 'id2', schema: 'banner'},
          {id: 'id3', schema: 'banner'},
        ],
        wrapperProps: {
            title: {
                text: 'Галарея баннеров',
                indent: '5'
            }
        },
        props: {
            height: 240,
            columns: 3,
            align: 'center',
        }
    };

    const state = {
      collections: {
          banner: {
              id1: {
                  entity: 'banner',
                  id: 'id1',
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
                  link: '/lego-new-products',
                  realLink: '/lego-new-products',
              },
              id2: {
                  entity: 'banner',
                  id: 'id2',
                  image: {
                      entity: 'picture',
                      thumbnail: {
                          entity: 'thumbnail',
                          width: '1920',
                          height: '300',
                          densities: [
                              {
                                  entity: 'density',
                                  id: 1,
                                  url: '//avatars.mds.yandex.net/get-market_banners/1653693/3093147_1.28653a8583b9eb8c33aeb77070abfde3.png.3093147/orig'
                              },
                              {
                                  entity: 'density',
                                  id: 2,
                                  url: '//avatars.mds.yandex.net/get-market_banners/1428676/3093147_4.feb43f55f6de2293a4e6810be53243c9.png.3093147/orig'
                              }
                          ]
                      }
                  },
                  link: '/catalog/konstruktory/78214/list?hid=10470548&utm_source=adfox_desktop&utm_medium=banner_regular&utm_campaign=beru_konstruktory_1504&glfilter=7893318%3A3732937%2C14619774&how=opinions',
                  realLink: '/catalog/konstruktory/78214/list?hid=10470548&utm_source=adfox_desktop&utm_medium=banner_regular&utm_campaign=beru_konstruktory_1504&glfilter=7893318%3A3732937%2C14619774&how=opinions',
              },
              id3: {
                  entity: 'banner',
                  id: 'id3',
                  image: {
                      entity: 'picture',
                      thumbnail: {
                          entity: 'thumbnail',
                          width: '1920',
                          height: '300',
                          densities: [
                              {
                                  entity: 'density',
                                  id: 1,
                                  url: '//avatars.mds.yandex.net/get-market_banners/1531347/3012636_1.abcdf7c0b0115a417b29ff7eb422d415.jpg.3012636/orig'
                              },
                              {
                                  entity: 'density',
                                  id: 2,
                                  url: '//avatars.mds.yandex.net/get-market_banners/1523118/3012636_4.b3759cfc90006a776ebe63568c1b9909.jpg.3012636/orig'
                              }
                          ]
                      }
                  },
                  link: '/catalog/konstruktory/78214/list?hid=10470548&utm_source=adfox_desktop&utm_medium=banner_regular&utm_campaign=beru_konstruktory_1504&glfilter=7893318%3A3732937%2C14619774&how=',
                  realLink: '/catalog/konstruktory/78214/list?hid=10470548&utm_source=adfox_desktop&utm_medium=banner_regular&utm_campaign=beru_konstruktory_1504&glfilter=7893318%3A3732937%2C14619774&how=',
              }
          }
      }
  }

   const store = createStore(() => state);

   <Provider store={store}>
       <div style={{
           width: 800,
           height: 350,
           overflow: 'hidden',
           padding: '10px',
           background: 'grey',
       }}>
           {withWidgetWrapper(View)(props)}
       </div>
   </Provider>
```
