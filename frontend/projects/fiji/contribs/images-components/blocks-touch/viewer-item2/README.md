# viewer-item2

Контейнер для картинки в просмотрщике для тач-устройств.

<a name="mods"></a>
### Модификаторы блока

| Модификатор | Значения | Способы установки | Описание |
| ----------- | -------- | ----------------- | -------- |
| `[active]` | `yes` | `JS` | Устанавливает контейнер текущим (видимым). |
| `[progress]` | `yes` | `JS` | Отображает загрузку данных в контейнере. |
| `[error]` | `yes` | `JS` | Показывает сообщение об ошибке загрузки картинки. |
| `[fullscreen]` | `yes` | `image-touch-viewer2_fullscreen-enable_yes.deps.js`, `JS` | Включает полноэкранный режим. |

### Приватные модификаторы блока
| Модификатор | Значения | Способы установки | Описание |
| ----------- | -------- | ----------------- | -------- |
| `content` | `no` | `images-touch-viewer2_content_no.deps.js` | Контейнер без скролла. |
| `content` | `yes` | `images-touch-viewer2_content_yes.deps.js` | Контейнер со скроллом. |
| `[carousel]` | `yes` | `viewer-carousel2__list.deps.js`, `BEMJSON` | Добавляет стрелки листания карусели. |
| `[progress-enable]` | `yes` | `images-touch-viewer2_progress-enable_yes.deps.js`, `BEMJSON` | Включает возможность отображения загрузки данных в контейнере. |
| `[fullscreen]` | `yes` | `images-touch-viewer2_fullscreen_yes.deps.js` | Реагирует на событие включения полноэкранного режима. |
| `[scale-enable]` | `yes` | `images-touch-viewer2_scale-enable_yes.deps.js`, `BEMJSON` | Увеличивает картинку при жестах двумя пальцами и двойном тапе. |
| `[scaled]` | `yes` | `JS` | Сообщает о том, что картинка увеличена. Не имеет `js`\|`css` реализации. |
