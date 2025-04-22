# @yandex-fleet/metrika

The utility package to log events to [Yandex.Metrika](https://metrika.yandex.ru/).

## Goal rules

1. One section - one goal.
2. Goal's name === section's name.
3. Create a separate file for each section in `src/goals`.
4. Property `action` is obligatory. `Action` consists of two parts:

- full element description (e.g., `hint`, `chart_orders`, `button_close`),
- event name (e.g., `clicked`, `opened`, `hovered`).
  Thus, the full name is `hint_hovered`, `chart_orders_clicked`, `button_close_clicked`.

4. Put a documentation comment near each action which clearly describes the purpose of the action.
5. Add link to the analytics ticket that describes metrika goals at the beginning of the file in `src/goals/<filename>`.
6. Use snake case for goal description.

## Goal definition

1. Create new file in `src/goals`.
2. Add goal definition:

```ts
type SectionGoal = {
  /** @description click on the button closing the modal */
  action: "button_clicked";
  is_opened: boolean;
};
```

3. Update type `Goals` in `useReachGoal.ts` with new goal.

## Usage

```tsx
import { useReachGoal } from "@yandex-fleet/metrika";

const Component = () => {
  const [open, setOpen] = useState(false);
  const reachGoal = useReachGoal("section");

  return (
    <button
      onClick={() => {
        setOpen((prev) => !prev);
        reachGoal({
          action: "button_clicked",
          is_opened: !open,
        });
      }}
    />
  );
};
```

## Debugging

<https://yandex.ru/support/metrica/general/check-counter.html#check-counter>
