# FeedbackButton

Кнопка в виде жука для открытия формы из сервиса [Яндекс.Формы](https://forms.yandex-team.ru) в модальном окне. В
основном это используется для форм обратной связи.

Есть яндексовая альтернатива [Жучок](https://wiki.yandex-team.ru/bughunter/bugs/).
`FeedbackButton`, кажется, проще и легче.

## Props

| Свойство       | Тип           | Умолчание     | Описание                                       |
| :------------- | :------------ | :------------ | :--------------------------------------------- |
| `cls?`         | `string`      | `''`          | Класс CSS                                      |
| `formId`       | `number`      | `-`           | ID формы в Яндекс.Формы                        |
| `title`        | `string`      | `-`           | Заголовок модального окна                      |
| `globalHotkey` | `IKey / null` | `{code:'F1'}` | Горячая клавиша для вызова: `null` - отключить |

## Пример

```tsx
import { FeedbackButton } from '@yandex-infracloud-ui/libs';

function Example() {
   return <FeedbackButton formId={22776} title='Есть вопрос?' />;
}
```

<!-- STORY -->
