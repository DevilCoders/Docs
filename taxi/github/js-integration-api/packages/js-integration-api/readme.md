## Установка
    npm install @yandex-taxi/js-integration-api --save

## Использование

❗Внимание❗ **headers** в клиенте устанавливать обязательно.

#### `fetch` клиент
```javascript
import {create, SourceID} from '@yandex-taxi/js-integration-api'

const client = async (url, options) => {
  const {
    body,
    headers,
  } = options
  const response = await fetch(url, {
    headers,
    method: 'post',
    body: JSON.stringify(body),
  })

  return await response.json()
}

const api = create({
  meta: {
    sourceId: SourceID.WIZARD,
  },
  client,
})

// использование
api.profile(body)
  .then(data => console.log(data))
```

#### `XMLHttpRequest` клиент
```javascript
import {create, SourceID} from '@yandex-taxi/js-integration-api'

const client = (url, { body, headers }, onSuccess, onError) => {
  const xhr = new XMLHttpRequest()

  xhr.open('POST', url, true)
  Object.entries(headers).map(([name, value]) => {
    xhr.setRequestHeader(name, value)
  })
  xhr.addEventListener('load', e => {
    const data = e.target
      ? JSON.parse(e.target.response)
      : undefined

    onSuccess(data)
  })
  xhr.addEventListener('error', (e) => onError(e.target))
  xhr.send(JSON.stringify(body))
}

const api = create({
  meta: {
    sourceId: SourceID.ALICE,
  },
  client,
})

// использование
const success = data => console.log(data)
const fail = error => console.error(error)

api.profile(body, success, fail)
```

Все методы, возвращаемые функцией `create` принимают первым аргументом тело запроса, остальные прокидываются в `client` как есть.

## Релиз
    npm run release
    git push --follow-tags origin master && npm publish
