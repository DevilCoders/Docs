Стандартная фатальная ошибка на сервисе

```jsx
  import Text from '@self/root/src/uikit/components/Text';
  const {ERROR_ZERO_SAD_ICECREAM} = require('@self/root/src/constants/imageUrls');
  const Provider = require('react-redux').Provider;
  const createStore = require('redux').createStore;
  const store = createStore(() => ({
      collections: {},
  }));

  <Provider store={store}>
      <div>
          <Text>400-ошибка</Text>
          <FatalError code={400}/>

          <hr/>
          <br/>
          <br/>
          <Text>403-ошибка</Text>
          <FatalError code={403}/>

          <hr/>
          <br/>
          <br/>

          <Text>404-ошибка</Text>
          <FatalError code={404}/>

          <hr/>
          <br/>
          <br/>

          <Text>500-ошибка</Text>
          <FatalError code={500}/>

          <hr/>
          <br/>
          <br/>

          <Text>Кастомная ошибка</Text>

          <div style={{
            display: 'flex',
            justifyContent: 'center',
            margin: '68px auto',
          }}>
              <FatalError
                  position={'horizontal'}
                  code={500}
                  imageSrc={ERROR_ZERO_SAD_ICECREAM}
                  imageSize={164}
                  title={'Что-то пошло не так'}
                  message={[
                      'Произошла техническая ошибка.',
                      'Попробуйте ещё раз.'
                  ]}

                  actions={[
                      'refresh'
                  ]}
              />
          </div>
      </div>

  </Provider>
```
