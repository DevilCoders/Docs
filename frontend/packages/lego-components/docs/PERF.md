# Производительность

При разработке новых компонентов и улучшении существующих  необходимо учитывать:

* Быстроту серверного и клиентского рендеринга
* Размер html-разметки при серверном рендеринге
* Минимальное количество dom-узлов

Для выполнения этих пунктов можно воспользоваться следующими инструментами:

## React devtools

Для проверки производительности можно воспользоваться браузерным расширением [react-devtools][react-devtools].

### trace

Планировщик react предоставляет [trace API][trace-api] позволяющий замерить время выполнения функций при различных взаимодействиях:

```ts
import { unstable_trace as trace } from 'scheduler/tracing'

class MyComponent extends Component {
  handleLoginButtonClick = (event) => {
    trace('Login button click', performance.now(), () => {
      this.setState({ isLoggingIn: true })
    })
  }

  // render ...
}
```

## Storybook

Для проверки производительности используется [storybook-addon-performance][storybook-addon-performance], а так же собственный декоратор, который более точно рассчитывает время клиентского рендеринга.

На какие метрики стоит обращать внимание:

### server

* **Render to string** — Время серверного рендеринга
* **String output size (gzip)** — Размер html-разметки которая приходит с сервера

### client

* **Initial render** — Время клиентского рендеринга (показывает не совсем точный результат, из-за обвязок сторибука, поэтому стоит смотреть в devtools-консоль для получения более точного результата)
* **DOM element count** — Количество DOM-узлов после рендеринга компонента

## Benchmark

Soon.

[storybook-addon-performance]: https://github.com/atlassian-labs/storybook-addon-performance
[react-devtools]: https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
[trace-api]: https://gist.github.com/bvaughn/8de925562903afd2e7a12554adcdda16
