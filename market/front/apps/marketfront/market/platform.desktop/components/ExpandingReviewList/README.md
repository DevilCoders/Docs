# ExpandingReviewList

Список отзывов или оценок с юзером(аватар, имя, бейдж "Проверенный покупатель"), оценкой и датой

Пример использования:
```jsx
import ExpandingReviewList from '@self/platform/components/ExpandingReviewList';

const reviews = [{
        reviewId: 1034156,
    }];
const title = 'Отзывы';

<ExpandingReviewList reviews={reviews} title={title}/>

```

Пример использования с контейнером:
```jsx
import ExpandingReviewList from '@self/platform/containers/ExpandingReviewList';

const reviewsIds = [59145917];
const title = 'Отзывы';

<ExpandingReviewList reviewsIds={reviewsIds}/>

```
