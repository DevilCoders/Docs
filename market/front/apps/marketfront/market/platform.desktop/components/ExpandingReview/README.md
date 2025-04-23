# ExpandingReview

Раскрывающийся блок отзыва

Содержит текст отзыва(если есть), имя и аватар пользователя
и бейдж "Проверенный покупатель"(если есть), дату и общую оценку.

Отображается с кнопками "Читать далее"/"Свернуть", если текст отзыва
превышает заданную константу(default 300 символов)

Пример использования:
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const reviewText = 'test string';
const reviewDate = '3 сентября';
const averageGrade = 4;
const userId = 0;
const anonymous = 0;
const cpa = true;

<Provider store={store}>
    <ExpandingReview
        reviewText={reviewText}
        averageGrade={averageGrade}
        userId={userId}
        anonymous={anonymous}
        cpa={cpa}
        reviewDate={reviewDate}
    />
</Provider>
```
