## Тестирование HOC'ов

```jsx
import Mocks from 'spec/mocks'

import withSomething from './withSomething'

describe('withSomething', () => {
  it('should test something withSomething', () => {
    const {BaseComponent} = Mocks

    const Enhanced = withSomething(BaseComponent)

    mount(<Enhanced />)

    /**
     * BaseComponent.props дает доступ к полученным от хока пропсам
     */
    expect(BaseComponent.props.propFromHOC).to...

    /**
     * Таким образом можем дергать хендлеры и смотреть на изменения пропсов
     */
    BaseComponent.props.handlerFromHOC()
    expect(BaseComponent.props.anotherPropFromHOC).to...

    /**
     * А можем менять внешние пропсы компонента и смотреть, что в итоге получили
     */
    Enhanced.setProps({propForHOC: true})
    expect(BaseComponent.props.propFromHOC).to...
  })
})

```
