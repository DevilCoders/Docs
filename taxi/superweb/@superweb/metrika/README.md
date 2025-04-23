# @superweb/metrika

Yandex Metrika package

## Usage

```tsx
import { useMetrika } from "@superweb/metrika";

function App({ counterId }) {
  const { reachGoal } = useMetrika(counterId);

  return <button onClick={() => reachGoal("button_clicked")}>Click me</button>;
}
```

## Debugging

<https://yandex.ru/support/metrica/general/check-counter.html#check-counter>
