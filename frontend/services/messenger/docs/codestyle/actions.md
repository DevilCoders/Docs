# Кодстайл Actions

## Обычные экшены
1. Располагаются в `store/`: `store/chat.ts`.
2. Импортируются через namespace с суффиксом `Actions`: `import * as ChatActions from '../store/chat';`.

## Thunk экшены
1. Располагаются в `actions/`: `actions/Chat.ts`. В будущем переедем в `thunk/`: `thunk/chat.ts`.
2. Импортируются через namespace с суффиксом `Thunks`: `import * as ChatThunks from '../actions/chat';`.
