# Как создать f-react ibem-блок из React компонента?
1. Создать React компонент.
2. Импортировать его [здесь](../../../src/index.tsx "femida/src/index.tsx") по аналогии с другими компонентами.
3. Создать f-react ibem-блок с полями:<br>
   `block: 'f-react',`<br>
   `name: 'название_react_компонента',`<br>
   [Пример](../f-uxfeedback/f-uxfeedback.bemhtml.js "femida/blocks/desktop/f-uxfeedback/f-uxfeedback.bemhtml.js")
4. Добавить f-react в зависимости:<br>
    `mustDeps: [{ block: 'f-react' }]`<br>
   [Пример](../f-uxfeedback/f-uxfeedback.deps.js "femida/blocks/desktop/f-uxfeedback/f-uxfeedback.deps.js")
5. Теперь вы можете пользоваться вашим новым ibem-блоком!

