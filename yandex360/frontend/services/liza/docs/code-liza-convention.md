# Фичи
## Промки и уведомления
После задачи новых нотификаций https://st.yandex-team.ru/DARIA-62893 мы верстаем промки по гайдам от лего, сверстанным для почты, смотрим сюда и показываем дизайнерам:
https://lego-staging.dev.yandex-team.ru/islands/pull-4314/desktop.react-examples/message/all/all.html
https://st.yandex-team.ru/ISL-5084

Для темной темы используем белые промки, для светлых - черные.

Технология: только lego-on-react + react, используем в качестве примеров промо нотификаций. (Ждем lego-components)

## Метрика

1) При разработке метрики пишем ее на английском (см. https://st.yandex-team.ru/DARIA-65654), для оптимизации и укорачивания запросов в сервис
2) Если метрика показа элемента должна вызываться один раз, используем стандартные механизмы (функция `_.once`) или если стандартных механизмов недостаточно, функцию единоразового вызова метрики `Daria.memoizeById` (см. https://github.yandex-team.ru/personal-services/frontend/blob/dev/services/liza/client/modules/common/lib/memoizeById.js)

# React, mobx

## Локализация компонентов
В реакт компонентах следует всё использовать I18N компонент и переносить ключи в танкере. Иначе мы от i18n функции не избавимся.Организация ключей в реактовом I18N позволяет использовать более короткие ключи, т.к. ключи реакта группируются по keyset, а не сваливаются в одно хранилище.
Если трогаем старый реакт-компонент и особенно его ключи, и там используется функция i18n, заменяем ее на I18N.

## Реакции @reaction
В коде есть несколько способов создания и уничтожения реакций:
- создание через reaction(...) + уничтожение через функцию-дебаунсер https://mobx.js.org/refguide/reaction.html
- создание через reaction(...) + уничтожение через внутренний класс Disposer (пример https://github.yandex-team.ru/personal-services/frontend/blob/dev/services/liza/client/modules/compose-react-mobx/components/Signatures/SignaturesPopup.js#L84)
- создание через класс ReactionBase + функцию cancel

Настоятельно рекомендуется создавать реакции через стандартный механизм создания реакций в mobx. Текущая реализация реакции через ReactionBase выглядит атавизмом и может в теории не работать если в реакциях в новой версии mobx поменяется что-то.

## Порядок расположения свойств, методов в классах
Настоятельно рекомендуется располагать методы, свойства и прочие списки по алфавиту в первую очередь, а в рамках одного контекста по смыслу. Для чего - чтобы при мержах было меньше конфликтов и приятнее для перфекционистов.

## Использование событий
Если нужно передавать информацию из компонента в компонент, то предпочтительнее пользоваться mobx стейтом и отслеживанием изменения в целевом компоненте. Например если кликнули по кнопке, то промка должна закрыться. Можно кинуть событие в кнопке и отслеживать его в промо. А лучше - в mobx стейте иметь некоторое поле, меняющий значение статуса закрыто промо или нет. И в промо его менять. Как только поле поменялось - дергать в mobx стейте метод, закрывающий промо (примерно так). Идея в том, что использовать максимально mobx абстракции.
Если нужно реагировать на ns события, являющиеся мостом между реакт компонентами и ns видами, то триггер/вызов таких событий лучше вынести в mobx абстракцию, и использовать ее.

# lodash
Импортим весь lodash сразу.
Лучше

`import _ from 'lodash'`

Чем

`import escape from 'lodash/escape'`

# Написание кода
[Учитываем практики отсюда](https://github.yandex-team.ru/Daria/docs/blob/master/best-practices/js.md)

[JS codestyle и соглашения](https://github.yandex-team.ru/Daria/docs/tree/master/codestyle/javascript)
