[![Build status][2]][1]

  [1]: https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Disk_Web_ReactTanker_TestPr&branch_Disk_Web_ReactTanker=%3Cdefault%3E&tab=buildTypeStatusDiv
  [2]: https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Disk_Web_ReactTanker_TestPr)/statusIcon.svg (Go To Build Page)


## Локализация из Танкера с Reactjs

Реакт-компонента и небольшая библиотека, которая позволяет локализовывать проекты написанные на Реакте.

Библиотека написана на ES6. На NodeJs запускается без сборки. Предполагается, что на клиенте будет подключен babel с соответствующими трансформами.

### Быстрый старт

Сперва нужно скачать локализацию из танкера с помощью [небольшой утилиты tanker-fetch](https://github.yandex-team.ru/UFO/tanker-fetch). На выходе получаем по js-файлику на каждый язык, с которым умеет работать `react-tanker`

```jsx
import { addTranslation, setTankerProjectId, I18N } from 'react-tanker';

setTankerProjectId('yandex_disk_widget_save');
addTranslation('ru', require('loc.ru.js'));

ReactDOM.render(<I18N lang="ru" keyset="auth" loc="dont_remember_me" />, document.getElementById('app'));
```

### Ключи с параметрами

Используя **АПИ Танкера**

```jsx
// Файл «<i18n:param>name</i18n:param>» удалён
<I18N lang="ru" keyset="test" loc="file_name_deleted" name="Readme.md" />
```

### Вложенные реакт-элементы

Используя **кастомный XML в Танкере**. Тег вида `<x-{data-ref}>` заменяется на найденный среди деток элемент, ищется элемент по `data-ref`.

```jsx
// Файл «<i18n:param>name</i18n:param>» удалён в <x-trash-link>Корзину</x-trash-link>
<I18N lang="ru" keyset="test" loc="file_name_deleted" name="Readme.md">
    <a data-ref="trash-link" href="#trash"/>
</I18N>
```

```jsx
// Press <x-key>Ctrl</x-key>+<x-key>S</x-key>
<I18N lang="ru" keyset="test" loc="save_hint">
    <kbd data-ref="key"/>
</I18N>
```

В качестве исключения можно использовать тег `<br/>`.

```jsx
// Строка 1<br/>Строка 2<br/>Строка три
<I18N lang="ru" keyset="test" loc="text_with_br"/>
```
