```jsx
const pages = [
    {
      number: 1,
      url: '/page-route?page=1',
      active: false,
    },
    {
      number: 2,
      url: '',
      active: true,
    },
    {
      number: 3,
      url: '/page-route?page=3',
      active: false,
    },
    {
      number: 4,
      url: '/page-route?page=4',
      active: false,
    },
];
const prevPage = {
    number: 1,
    url: '/page-route?page=1',
    active: false,
};
const nextPage = {
    number: 3,
    url: '/page-route?page=3',
    active: false,
};
const onMoveToPage = (pageNumber) => {
    // make request for new page data
};

<Paginator
    pages={pages}
    prevPage={prevPage}
    nextPage={nextPage}
    onMoveToPage={onMoveToPage}
/>
```
